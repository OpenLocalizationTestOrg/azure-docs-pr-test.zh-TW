---
title: "備份 Azure 匯入/匯出磁碟機資訊清單 | Microsoft Docs"
description: "了解如何自動備份 Microsoft Azure 匯入/匯出服務的磁碟機資訊清單。"
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 594abd80-b834-4077-a474-d8a0f4b7928a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 33eb8e1eea8f8aa7b79ef3e54f2b1ed88dc794ae
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="backing-up-drive-manifests-for-azure-importexport-jobs"></a><span data-ttu-id="a9461-103">備份 Azure 匯入/匯出作業的磁碟機資訊清單</span><span class="sxs-lookup"><span data-stu-id="a9461-103">Backing up drive manifests for Azure Import/Export jobs</span></span>

<span data-ttu-id="a9461-104">可以藉由在 [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) 或 [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) REST API 作業中將 `BackupDriveManifest` 屬性設定為 `true`，將磁碟機資訊清單自動備份到 blob。</span><span class="sxs-lookup"><span data-stu-id="a9461-104">Drive manifests can be automatically backed up to blobs by setting the `BackupDriveManifest` property to `true` in the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) REST API operations.</span></span> <span data-ttu-id="a9461-105">根據預設，不會備份磁碟機資訊清單。</span><span class="sxs-lookup"><span data-stu-id="a9461-105">By default, the drive manifests are not backed up.</span></span> <span data-ttu-id="a9461-106">磁碟機資訊清單備份會在與工作相關聯的儲存體帳戶內，在容器中儲存為區塊 Blob。</span><span class="sxs-lookup"><span data-stu-id="a9461-106">The drive manifest backups are stored as block blobs in a container within the storage account associated with the job.</span></span> <span data-ttu-id="a9461-107">根據預設，容器名稱是 `waimportexport`，但是您可以在呼叫 `Put Job` 或 `Update Job Properties` 作業時，於 `DiagnosticsPath` 屬性中指定不同的名稱。</span><span class="sxs-lookup"><span data-stu-id="a9461-107">By default, the container name is `waimportexport`, but you can specify a different name in the `DiagnosticsPath` property when calling the `Put Job` or `Update Job Properties` operations.</span></span> <span data-ttu-id="a9461-108">備份資訊清單 blob 會以下列格式命名︰`waies/jobname_driveid_timestamp_manifest.xml`。</span><span class="sxs-lookup"><span data-stu-id="a9461-108">The backup manifest blob are named in the following format: `waies/jobname_driveid_timestamp_manifest.xml`.</span></span>

 <span data-ttu-id="a9461-109">您可以藉由呼叫 [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) 作業來擷取工作的備份磁碟機資訊清單 URI。</span><span class="sxs-lookup"><span data-stu-id="a9461-109">You can retrieve the URI of the backup drive manifests for a job by calling the [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="a9461-110">會在每個磁碟機的 `ManifestUri` 屬性中傳回 Blob URI。</span><span class="sxs-lookup"><span data-stu-id="a9461-110">The blob URI is returned in the `ManifestUri` property for each drive.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a9461-111">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a9461-111">Next steps</span></span>

* [<span data-ttu-id="a9461-112">使用匯入/匯出服務 REST API</span><span class="sxs-lookup"><span data-stu-id="a9461-112">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
