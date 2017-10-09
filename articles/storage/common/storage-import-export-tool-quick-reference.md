---
title: "Azure 匯入/匯出工具匯入作業命令的 aaaQuick 參考 |Microsoft 文件"
description: "適用於常用匯入作業命令的 Azure 匯入/匯出工具命令參考。"
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 35e46f24f764a5098ca465adb51badcab2d13e9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a><span data-ttu-id="4494a-103">匯入作業的常用命令快速參考</span><span class="sxs-lookup"><span data-stu-id="4494a-103">Quick reference for frequently used commands for import jobs</span></span>

<span data-ttu-id="4494a-104">本文章提供一些常用命令的快速參考。</span><span class="sxs-lookup"><span data-stu-id="4494a-104">This article provides a quick reference for some frequently used commands.</span></span> <span data-ttu-id="4494a-105">如需詳細使用方式，請參閱[針對匯入作業準備硬碟](../storage-import-export-tool-preparing-hard-drives-import.md)。</span><span class="sxs-lookup"><span data-stu-id="4494a-105">For detailed usage, see [Preparing Hard Drives for an Import Job](../storage-import-export-tool-preparing-hard-drives-import.md).</span></span>

## <a name="first-session"></a><span data-ttu-id="4494a-106">第一個工作階段</span><span class="sxs-lookup"><span data-stu-id="4494a-106">First session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1 /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

## <a name="second-session"></a><span data-ttu-id="4494a-107">第二個工作階段</span><span class="sxs-lookup"><span data-stu-id="4494a-107">Second session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2 /DataSet:dataset-2.csv
```

## <a name="abort-latest-session"></a><span data-ttu-id="4494a-108">中止最近的工作階段</span><span class="sxs-lookup"><span data-stu-id="4494a-108">Abort latest session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2 /AbortSession
```

## <a name="resume-latest-interrupted-session"></a><span data-ttu-id="4494a-109">繼續最近中斷的工作階段</span><span class="sxs-lookup"><span data-stu-id="4494a-109">Resume latest interrupted session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#3 /ResumeSession
```

## <a name="add-drives-toolatest-session"></a><span data-ttu-id="4494a-110">新增磁碟機 toolatest 工作階段</span><span class="sxs-lookup"><span data-stu-id="4494a-110">Add drives toolatest session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#3 /AdditionalDriveSet:driveset-2.csv
```

## <a name="next-steps"></a><span data-ttu-id="4494a-111">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4494a-111">Next steps</span></span>

* [<span data-ttu-id="4494a-112">匯入工作的範例工作流程 tooprepare 硬碟機</span><span class="sxs-lookup"><span data-stu-id="4494a-112">Sample workflow tooprepare hard drives for an import job</span></span>](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow.md)
