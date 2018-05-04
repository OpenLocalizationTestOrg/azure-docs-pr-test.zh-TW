---
title: "Azure SQL Database 的資料表稽核、TDS 重新導向及 IP 端點 | Microsoft Docs"
description: "了解在 Azure SQL Database 中實作資料表稽核時的稽核、TDS 重新導向及 IP 端點變更。"
services: sql-database
documentationcenter: 
author: giladm
manager: jhubbard
editor: 
ms.assetid: 4ef19ed1-e798-43a2-ad99-0e563f93ab53
ms.service: sql-database
ms.custom: security
ms.workload: On Demand
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: giladm
ms.openlocfilehash: 42c89f09eee4394fec7d2f33f51ddc5875587530
ms.sourcegitcommit: e5355615d11d69fc8d3101ca97067b3ebb3a45ef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/31/2017
---
# <a name="sql-database----downlevel-clients-support-and-ip-endpoint-changes-for-table-auditing"></a>SQL Database - 資料表稽核的舊版用戶端支援與 IP 端點變更

> [!IMPORTANT]
> 本文件僅適用於資料表稽核，也就是**現已淘汰**。<br>
> 請使用新的 [Blob 稽核](sql-database-auditing.md)方法，**不**需要修改舊版用戶端連接字串。 Blob 稽核的其他資訊位在[開始使用 SQL Database 稽核](sql-database-auditing.md)。

[資料庫稽核](sql-database-auditing.md)可自動與支援 TDS 重新導向的 SQL 用戶端搭配運作。 請注意，使用「Blob 稽核」方法時，不適用重新導向。

## <a id="subheading-1"></a>舊版用戶端支援
實作 TDS 7.4 的任何用戶端應該也支援重新導向。 例外包括其中未完全支援重新導向功能的 JDBC 4.0，和其中未實作重新導向的 Tedious for Node.JS。

對於「舊版用戶端」，也就是支援 TDS 7.3 版和以下版本 - 應該修改連接字串中的伺服器 FQDN：

連接字串中的原始伺服器 FQDN：<*伺服器名稱*>.database.windows.net

連接字串中已修改的伺服器 FQDN：<*伺服器名稱*>.database.**secure**.windows.net

「舊版用戶端」的部分清單包括：

* .NET 4.0 和以下版本，
* ODBC 10.0 和以下版本。
* JDBC (雖然 JDBC 支援 TDS 7.4，但並未完整支援 TDS 重新導向功能)
* Tedious (適用於 Node.JS)

**備註：** 上述伺服器 FDQN 修改可能會對於套用 SQL Server 層級稽核原則有所助益，不需要每個資料庫中的組態步驟 (暫存緩和)。

## <a id="subheading-2"></a>啟用稽核的 IP 端點變更
請注意，當您啟用「資料表稽核」時，您資料庫的 IP 端點將會變更。 如果您有嚴格的防火牆設定，請適當更新這些防火牆設定。

新的資料庫 IP 端點將取決於資料庫區域：

| 資料庫區域 | 可能的 IP 端點 |
| --- | --- |
| 中國北部 |139.217.29.176, 139.217.28.254 |
| 中國東部 |42.159.245.65, 42.159.246.245 |
| 澳洲東部 |104.210.91.32, 40.126.244.159, 191.239.64.60, 40.126.255.94 |
| 澳洲東南部 |191.239.184.223, 40.127.85.81, 191.239.161.83, 40.127.81.130 |
| 巴西南部 |104.41.44.161, 104.41.62.230, 23.97.99.54, 104.41.59.191 |
| 美國中部 |104.43.255.70, 40.83.14.7, 23.99.128.244, 40.83.15.176 |
| 美國中部 EUAP |52.180.178.16, 52.180.176.190 |
| 東亞 |23.99.125.133, 13.75.40.42, 23.97.71.138, 13.94.43.245 |
| 美國東部 2 |104.209.141.31, 104.208.238.177, 191.237.131.51, 104.208.235.50 |
| 美國東部 |23.96.107.223, 104.41.150.122, 23.96.38.170, 104.41.146.44 |
| 美國東部 EUAP |52.225.190.86, 52.225.191.187 |
| 印度中部 |104.211.98.219, 104.211.103.71 |
| 印度南部 |104.211.227.102, 104.211.225.157 |
| 印度西部 |104.211.161.152, 104.211.162.21 |
| 日本東部 |104.41.179.1, 40.115.253.81, 23.102.64.207, 40.115.250.196 |
| 日本西部 |104.214.140.140, 104.214.146.31, 191.233.32.34, 104.214.146.198 |
| 美國中北部 |191.236.155.178, 23.96.192.130, 23.96.177.169, 23.96.193.231 |
| 北歐 |104.41.209.221, 40.85.139.245, 137.116.251.66, 40.85.142.176 |
| 美國中南部 |191.238.184.128, 40.84.190.84, 23.102.160.153, 40.84.186.66 |
| 東南亞 |104.215.198.156, 13.76.252.200, 23.97.51.109, 13.76.252.113 |
| 西歐 |104.40.230.120, 13.80.23.64, 137.117.171.161, 13.80.8.37, 104.47.167.215, 40.118.56.193, 104.40.176.73, 40.118.56.20 |
| 美國西部 |191.236.123.146, 138.91.163.240, 168.62.194.148, 23.99.6.91 |
| 美國西部 2 |13.66.224.156, 13.66.227.8 |
| 美國中西部 |52.161.29.186, 52.161.27.213 |
| 加拿大中部 |13.88.248.106, 13.88.248.110 |
| 加拿大東部 |40.86.227.82, 40.86.225.194 |
| 英國北部 |13.87.101.18, 13.87.100.232 |
| 英國南部 2 |13.87.32.202, 13.87.32.226 |