---
title: "HDInsight 的 Azure 上的 aaaUnderstand 並解決 WebHCat 錯誤 |Microsoft 文件"
description: "了解如何在 HDInsight 上 WebHCat 傳回 tooabout 常見錯誤以及如何 tooresolve 它們。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1b3d94b1-207d-4550-aece-21dc45485549
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 0071a1e9ed448ae146b93c8f4f518e31b95d27c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-resolve-errors-received-from-webhcat-on-hdinsight"></a>了解並解決 HDInsight 上從 WebHCat 收到的錯誤

了解使用 HDInsight WebHCat 何時及如何所收到的錯誤 tooresolve 它們。 WebHCat 為內部使用的用戶端工具，例如 Azure PowerShell 和 hello Data Lake Tools for Visual Studio。

## <a name="what-is-webhcat"></a>什麼是 WebHCat？

[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) 是適用於 [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog) 的 REST API，這是 Hadoop 的資料表和儲存體管理層。 WebHCat HDInsight 叢集上的預設會啟用和使用各種工具 toosubmit 工作，而不記錄 toohello 叢集中取得作業狀態等。

## <a name="modifying-configuration"></a>修改組態

> [!IMPORTANT]
> 有幾個這份文件中所列的 hello 錯誤發生的原因已超過設定的上限。 當 hello 解決步驟提及您可以變更值時，您必須使用其中一個 hello tooperform hello 變更之後：

* 如**Windows**叢集： 在叢集建立期間使用指令碼動作 tooconfigure hello 值。 如需詳細資訊，請參閱 [開發指令碼動作](hdinsight-hadoop-script-actions.md)。

* 如**Linux**叢集： 使用 Ambari （web 或 REST API） toomodify hello 值。 如需詳細資訊，請參閱 [使用 Ambari 管理 HDInsight](hdinsight-hadoop-manage-ambari.md)

> [!IMPORTANT]
> Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。

### <a name="default-configuration"></a>預設組態

如果超過 hello 下列預設值，它可以降低 WebHCat 效能，或造成錯誤：

| 設定 | 作用 | 預設值 |
| --- | --- | --- |
| [yarn.scheduler.capacity.maximum-applications][maximum-applications] |hello 可以同時為作用中的作業數目上限 （暫止或執行） |10,000 |
| [templeton.exec.max-procs][max-procs] |hello 可以同時處理要求的數目上限 |20 |
| [mapreduce.jobhistory.max-age-ms][max-age-ms] |hello 的作業歷程記錄會保留天數 |7 天 |

## <a name="too-many-requests"></a>要求太多

**HTTP 狀態碼**：429

| 原因 | 解決方案 |
| --- | --- |
| 您已超過 hello 最大並行要求由 WebHCat 每分鐘 （預設值 20） |減少您不要未送出多個 hello 的並行要求數目上限或藉由修改提高 hello 並行要求限制您的工作負載 tooensure `templeton.exec.max-procs`。 如需詳細資訊，請參閱[修改組態](#modifying-configuration) 。 |

## <a name="server-unavailable"></a>無法使用伺服器

**HTTP 狀態碼**：503

| 原因 | 解決方案 |
| --- | --- |
| 此狀態碼，通常會發生在 hello 主要與次要資料庫之間的容錯移轉期間 hello 叢集前端節點 |等待兩分鐘，然後重試 hello 作業 |

## <a name="bad-request-content-could-not-find-job"></a>不正確的要求內容：找不到工作

**HTTP 狀態碼**：400

| 原因 | 解決方案 |
| --- | --- |
| 工作詳細資料已遭清除 hello 作業歷程記錄的清除器 |作業記錄的 hello 預設保留期限為 7 天。 要變更 hello 預設保留期限，請修改`mapreduce.jobhistory.max-age-ms`。 如需詳細資訊，請參閱[修改組態](#modifying-configuration) 。 |
| 作業已經刪除到期 tooa 容錯移轉 |重試作業提交向上 tootwo 分鐘 |
| 使用的工作識別碼無效 |請檢查是否正確 hello 作業識別碼 |

## <a name="bad-gateway"></a>閘道不正確

**HTTP 狀態碼**：502

| 原因 | 解決方案 |
| --- | --- |
| 內部記憶體回收發生在 hello WebHCat 程序 |等候記憶體回收集合 toofinish 或重新啟動 hello WebHCat 服務 |
| 逾時等候 hello ResourceManager 服務的回應。 當使用中的應用程式的 hello 數目變成 hello 設定最大值 （預設值 10000） 時，會發生這個錯誤 |等待目前執行的作業 toocomplete 或藉由修改提高 hello 並行工作限制`yarn.scheduler.capacity.maximum-applications`。 如需詳細資訊，請參閱 hello[修改組態](#modifying-configuration)> 一節。 |
| 嘗試透過 hello 的所有工作 tooretrieve [GET /jobs](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference+Jobs)時呼叫`Fields`太設定`*` |不要擷取*所有*作業詳細資料。 改用`jobid`tooretrieve 作業只大於特定的作業識別碼的詳細資料。或者，不要使用 `Fields` |
| 在前端節點容錯移轉期間 hello WebHCat 服務已關閉 |等待兩分鐘後再重試 hello 作業 |
| 有 500 個以上透過 WebHCat 提交的擱置工作 |等到目前擱置的工作完成，再送出更多工作 |

[maximum-applications]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.3/bk_system-admin-guide/content/setting_application_limits.html
[max-procs]: https://hive.apache.org/javadocs/hcat-r0.5.0/configuration.html
[max-age-ms]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.6.0/ds_Hadoop/hadoop-mapreduce-client/hadoop-mapreduce-client-core/mapred-default.xml
