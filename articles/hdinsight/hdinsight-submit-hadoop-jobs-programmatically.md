---
title: "在 HDInsight 上提交 Hadoop 工作 | Microsoft Docs"
description: "了解如何將 Hadoop 工作提交至 Azure HDInsight Hadoop。"
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 50430b96-2329-4775-9713-19c5795b775f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 6829ff82afc7fcea9e027ad14ec7ed0c8015a5fe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="submit-hadoop-jobs-in-hdinsight"></a><span data-ttu-id="0fd50-103">在 HDInsight 上提交 Hadoop 工作</span><span class="sxs-lookup"><span data-stu-id="0fd50-103">Submit Hadoop jobs in HDInsight</span></span>

<span data-ttu-id="0fd50-104">您可以使用 .NET SDK、Curl 和 Azure PowerShell 提交 Hadoop 作業：</span><span class="sxs-lookup"><span data-stu-id="0fd50-104">You can submit Hadoop jobs using .NET SDK, Curl, and Azure PowerShell:</span></span>

- <span data-ttu-id="0fd50-105">使用 .NET SDK</span><span class="sxs-lookup"><span data-stu-id="0fd50-105">Use .NET SDK</span></span>

  - [<span data-ttu-id="0fd50-106">建立非互動式驗證 .NET 應用程式</span><span class="sxs-lookup"><span data-stu-id="0fd50-106">Create non-interactive authentication .NET applications</span></span>](hdinsight-create-non-interactive-authentication-dotnet-applications.md)
  - [<span data-ttu-id="0fd50-107">使用 HDInsight .NET SDK 執行 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="0fd50-107">Run Hive queries using HDInsight .NET SDK</span></span>](hdinsight-hadoop-use-hive-dotnet-sdk.md)
  - [<span data-ttu-id="0fd50-108">在 HDInsight 中使用 .NET SDK for Hadoop 執行 Pig 作業</span><span class="sxs-lookup"><span data-stu-id="0fd50-108">Run Pig jobs using the .NET SDK for Hadoop in HDInsight</span></span>](hdinsight-hadoop-use-pig-dotnet-sdk.md)
  - [<span data-ttu-id="0fd50-109">在 HDInsight 中使用 .NET SDK for Hadoop 執行 Sqoop 作業</span><span class="sxs-lookup"><span data-stu-id="0fd50-109">Run Sqoop jobs using .NET SDK for Hadoop in HDInsight</span></span>](hdinsight-hadoop-use-sqoop-dotnet-sdk.md)
  - [<span data-ttu-id="0fd50-110">使用 HDInsight .NET SDK 執行 MapReduce 作業</span><span class="sxs-lookup"><span data-stu-id="0fd50-110">Run MapReduce jobs using HDInsight .NET SDK</span></span>](hdinsight-hadoop-use-mapreduce-dotnet-sdk.md)

- <span data-ttu-id="0fd50-111">CURL</span><span class="sxs-lookup"><span data-stu-id="0fd50-111">CURL</span></span>

  - [<span data-ttu-id="0fd50-112">使用 Curl 在 HDInsight 中以 Hadoop 執行 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="0fd50-112">Run Hive queries with Hadoop in HDInsight with Curl</span></span>](hdinsight-hadoop-use-hive-curl.md)
  - [<span data-ttu-id="0fd50-113">使用 Curl 搭配執行 Pig 作業與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="0fd50-113">Run Pig jobs with Hadoop on HDInsight by using Curl</span></span>](hdinsight-hadoop-use-pig-curl.md)
  - [<span data-ttu-id="0fd50-114">使用 Curl 在 HDInsight 中以 Hadoop 執行 Sqoop 作業</span><span class="sxs-lookup"><span data-stu-id="0fd50-114">Run Sqoop jobs with Hadoop in HDInsight with Curl</span></span>](hdinsight-hadoop-use-sqoop-curl.md)
  - [<span data-ttu-id="0fd50-115">使用 Curl 搭配執行 MapReduce 作業與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="0fd50-115">Run MapReduce jobs with Hadoop on HDInsight using Curl</span></span>](hdinsight-hadoop-use-mapreduce-curl.md)

- <span data-ttu-id="0fd50-116">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0fd50-116">PowerShell</span></span>

  - [<span data-ttu-id="0fd50-117">使用 PowerShell 執行 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="0fd50-117">Run Hive queries using PowerShell</span></span>](hdinsight-hadoop-use-hive-powershell.md)
  - [<span data-ttu-id="0fd50-118">使用 PowerShell 執行 Pig 作業</span><span class="sxs-lookup"><span data-stu-id="0fd50-118">Run Pig jobs using PowerShell</span></span>](hdinsight-hadoop-use-pig-powershell.md)
  - [<span data-ttu-id="0fd50-119">搭配使用 Sqoop 與 HDInsight 中的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="0fd50-119">Use Sqoop with Hadoop in HDInsight</span></span>](hdinsight-hadoop-use-sqoop-powershell.md)
  - [<span data-ttu-id="0fd50-120">使用 PowerShell 搭配執行 MapReduce 工作與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="0fd50-120">Run MapReduce jobs with Hadoop on HDInsight using PowerShell</span></span>](hdinsight-hadoop-use-mapreduce-powershell.md)

## <a name="see-also"></a><span data-ttu-id="0fd50-121">另請參閱</span><span class="sxs-lookup"><span data-stu-id="0fd50-121">See also</span></span>

- [<span data-ttu-id="0fd50-122">Azure HDInsight 文件</span><span class="sxs-lookup"><span data-stu-id="0fd50-122">Azure HDInsight Documentation</span></span>](https://docs.microsoft.com/azure/hdinsight/)