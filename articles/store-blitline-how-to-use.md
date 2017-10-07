---
title: "映像處理的 aaaHow toouse Blitline Azure 功能指南"
description: "了解 toouse hello Blitline 服務 tooprocess 映像，在 Azure 應用程式的方式。"
services: 
documentationcenter: .net
author: blitline-dev
manager: jason@blitline.com
editor: jason@blitline.com
ms.assetid: 6c711248-0e52-4895-ba9e-8395628de924
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/09/2014
ms.author: support@blitline.com
ms.openlocfilehash: 328fd177e25f45f29f8ad8e142d02b46017a858e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blitline-with-azure-and-azure-storage"></a><span data-ttu-id="bb47b-103">如何使用 Azure 和 Azure 儲存體 Blitline toouse</span><span class="sxs-lookup"><span data-stu-id="bb47b-103">How toouse Blitline with Azure and Azure Storage</span></span>
<span data-ttu-id="bb47b-104">本指南將說明如何 tooaccess Blitline 服務和 toosubmit 作業 tooBlitline 的方式。</span><span class="sxs-lookup"><span data-stu-id="bb47b-104">This guide will explain how tooaccess Blitline services and how toosubmit jobs tooBlitline.</span></span>

## <a name="what-is-blitline"></a><span data-ttu-id="bb47b-105">什麼是 Blitline？</span><span class="sxs-lookup"><span data-stu-id="bb47b-105">What is Blitline?</span></span>
<span data-ttu-id="bb47b-106">Blitline 是以雲端為基礎的影像，處理服務，可提供企業層級的映像處理 hello 價格它需要成本 toobuild 一部分在它自己。</span><span class="sxs-lookup"><span data-stu-id="bb47b-106">Blitline is a cloud-based image processing service that provides enterprise level image processing at a fraction of hello price that it would cost toobuild it yourself.</span></span>

<span data-ttu-id="bb47b-107">hello 事實是該映像處理已完成一再重複，通常從針對每個網站的 hello 地面重建。</span><span class="sxs-lookup"><span data-stu-id="bb47b-107">hello fact is that image processing has been done over and over again, usually rebuilt from hello ground up for each and every website.</span></span> <span data-ttu-id="bb47b-108">我們了解這個情況，那是因為我們已經建立了上百萬次。</span><span class="sxs-lookup"><span data-stu-id="bb47b-108">We realize this because we’ve built them a million times too.</span></span> <span data-ttu-id="bb47b-109">有一天，我們決定或許是替所有人執行此動作的時候了。</span><span class="sxs-lookup"><span data-stu-id="bb47b-109">One day we decided that perhaps it‘s time we just do it for everyone.</span></span> <span data-ttu-id="bb47b-110">我們已經知道如何 toodo toodo 它快速並有效率地與儲存每個人都適用於 hello 同時它。</span><span class="sxs-lookup"><span data-stu-id="bb47b-110">We know how toodo it, toodo it fast and efficiently, and save everyone work in hello meantime.</span></span>

<span data-ttu-id="bb47b-111">如需詳細資訊，請參閱 [http://www.blitline.com](http://www.blitline.com)(英文)。</span><span class="sxs-lookup"><span data-stu-id="bb47b-111">For more information, see [http://www.blitline.com](http://www.blitline.com).</span></span>

## <a name="what-blitline-is-not"></a><span data-ttu-id="bb47b-112">Blitline 不是什麼...</span><span class="sxs-lookup"><span data-stu-id="bb47b-112">What Blitline is NOT...</span></span>
<span data-ttu-id="bb47b-113">tooclarify 什麼 Blitline 是很有用，它是通常更容易 tooidentify Blitline 無法達成的目標之前繼續進行後續步驟。</span><span class="sxs-lookup"><span data-stu-id="bb47b-113">tooclarify what Blitline is useful for, it is often easier tooidentify what Blitline does NOT do before moving forward.</span></span>

* <span data-ttu-id="bb47b-114">Blitline 沒有 HTML widget tooupload 映像。</span><span class="sxs-lookup"><span data-stu-id="bb47b-114">Blitline does NOT have HTML widgets tooupload images.</span></span> <span data-ttu-id="bb47b-115">您必須提供的映像可公開或以供 Blitline tooreach 限制權限。</span><span class="sxs-lookup"><span data-stu-id="bb47b-115">You must have images available publicly or with restricted permissions available for Blitline tooreach.</span></span>
* <span data-ttu-id="bb47b-116">Blitline 不會執行即時影像處理，如 Aviary.com</span><span class="sxs-lookup"><span data-stu-id="bb47b-116">Blitline does NOT do live image processing, like Aviary.com</span></span>
* <span data-ttu-id="bb47b-117">Blitline 不接受映像上傳，您無法直接發送映像 tooBlitline。</span><span class="sxs-lookup"><span data-stu-id="bb47b-117">Blitline does NOT accept image uploads, you cannot push your images tooBlitline directly.</span></span> <span data-ttu-id="bb47b-118">您必須將其推送 tooAzure 儲存體或 Blitline 支援其他位置，然後告訴 Blitline toogo 哪裡取得它們。</span><span class="sxs-lookup"><span data-stu-id="bb47b-118">You must push them tooAzure Storage or other places Blitline supports and then tell Blitline where toogo get them.</span></span>
* <span data-ttu-id="bb47b-119">Blitline 可大量平行處理，但無法執行任何同步處理。</span><span class="sxs-lookup"><span data-stu-id="bb47b-119">Blitline is massively parallel and does NOT do any synchronous processing.</span></span> <span data-ttu-id="bb47b-120">這表示您必須提供 postback_url 給我們，我們會在處理完成時通知您。</span><span class="sxs-lookup"><span data-stu-id="bb47b-120">Meaning you must give us a postback_url and we can tell you when we are done processing.</span></span>

## <a name="create-a-blitline-account"></a><span data-ttu-id="bb47b-121">建立 Blitline 帳戶</span><span class="sxs-lookup"><span data-stu-id="bb47b-121">Create a Blitline account</span></span>
[!INCLUDE [blitline-signup](../includes/blitline-signup.md)]

## <a name="how-toocreate-a-blitline-job"></a><span data-ttu-id="bb47b-122">如何 toocreate Blitline 工作</span><span class="sxs-lookup"><span data-stu-id="bb47b-122">How toocreate a Blitline job</span></span>
<span data-ttu-id="bb47b-123">Blitline 會使用您想要在影像上的 tootake JSON toodefine hello 動作。</span><span class="sxs-lookup"><span data-stu-id="bb47b-123">Blitline uses JSON toodefine hello actions you want tootake on an image.</span></span> <span data-ttu-id="bb47b-124">此 JSON 是由幾個簡單欄位組合而成。</span><span class="sxs-lookup"><span data-stu-id="bb47b-124">This JSON is composed of a few simple fields.</span></span>

<span data-ttu-id="bb47b-125">hello 最簡單的範例如下所示：</span><span class="sxs-lookup"><span data-stu-id="bb47b-125">hello simplest example is as follows:</span></span>

        json : '{
       "application_id": "MY_APP_ID",
       "src" : "http://cdn.blitline.com/filters/boys.jpeg",
       "functions" : [ {
           "name": "resize_to_fit",
           "params" : { "width": 240, "height": 140 },
           "save" : { "image_identifier" : "external_sample_1" }
       } ]
    }'

<span data-ttu-id="bb47b-126">這裡我們有會"src 」 映像的 JSON"...boys.jpeg 」 再調整大小的影像 too240x140。</span><span class="sxs-lookup"><span data-stu-id="bb47b-126">Here we have JSON that will take a "src" image "...boys.jpeg" and then resize that image too240x140.</span></span>

<span data-ttu-id="bb47b-127">您可以在找到 hello 應用程式識別碼是您**連接資訊**或**管理**在 Azure 上的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="bb47b-127">hello Application ID is something you can find in your **CONNECTION INFO** or **MANAGE** tab on Azure.</span></span> <span data-ttu-id="bb47b-128">它是您的秘密識別碼，可讓您在 Blitline 的 toorun 作業。</span><span class="sxs-lookup"><span data-stu-id="bb47b-128">It is your secret identifier that allows you toorun jobs on Blitline.</span></span>

<span data-ttu-id="bb47b-129">[儲存] 參數的 hello 識別您希望我們已經處理它，一旦 tooput hello 映像的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="bb47b-129">hello "save" parameter identifies information about where you want tooput hello image once we have processed it.</span></span> <span data-ttu-id="bb47b-130">在這個簡單的案例中，我們尚未定義一個位置。</span><span class="sxs-lookup"><span data-stu-id="bb47b-130">In this trivial case, we haven't defined one.</span></span> <span data-ttu-id="bb47b-131">如果沒有定義位置，Blitline 會將它儲存在本機 (並暫時地) 的唯一雲端位置。</span><span class="sxs-lookup"><span data-stu-id="bb47b-131">If no location is defined Blitline will store it locally (and temporarily) at a unique cloud location.</span></span> <span data-ttu-id="bb47b-132">您將無法從 hello JSON 的位置時請 hello Blitline Blitline 傳回的 tooget。</span><span class="sxs-lookup"><span data-stu-id="bb47b-132">You will be able tooget that location from hello JSON returned by Blitline when you make hello Blitline.</span></span> <span data-ttu-id="bb47b-133">hello 「 映像 」 識別項需要並傳回 tooyou tooidentify 這個特定儲存映像時。</span><span class="sxs-lookup"><span data-stu-id="bb47b-133">hello "image" identifier is required and is returned tooyou when tooidentify this particular saved image.</span></span>

<span data-ttu-id="bb47b-134">您可以找到更多資訊 hello*函式*我們這裡支援： <http://www.blitline.com/docs/functions></span><span class="sxs-lookup"><span data-stu-id="bb47b-134">You can find more information about hello *functions* we support here: <http://www.blitline.com/docs/functions></span></span>

<span data-ttu-id="bb47b-135">您也可以尋找文件中的有關 hello 這裡工作選項： <http://www.blitline.com/docs/api></span><span class="sxs-lookup"><span data-stu-id="bb47b-135">You can also find documentation about hello job options here: <http://www.blitline.com/docs/api></span></span>

<span data-ttu-id="bb47b-136">一旦您的 JSON 時只需 toodo **POST**它太`http://api.blitline.com/job`</span><span class="sxs-lookup"><span data-stu-id="bb47b-136">Once you have your JSON all you need toodo is **POST** it too`http://api.blitline.com/job`</span></span>

<span data-ttu-id="bb47b-137">您將取回如下所示的 JSON：</span><span class="sxs-lookup"><span data-stu-id="bb47b-137">You will get JSON back that looks something like this:</span></span>

    {
     "results":
         {"images":
            [{
              "image_identifier":"external_sample_1",
              "s3_url":"https://s3.amazonaws.com/dev.blitline/2011110722/YOUR_APP_ID/CK3f0xBF_2bV6wf7gEZE8w.jpg"
            }],
          "job_id":"4eb8c9f72a50ee2a9900002f"
         }
    }


<span data-ttu-id="bb47b-138">這會告訴您，Blitline 已收到您的要求、 將它已將其放在處理佇列中，而 hello 映像完成後將會位於： **https://s3.amazonaws.com/dev.blitline/2011110722/YOUR\_應用程式\_識別碼/CK3f0xBF_2bV6wf7gEZE8w.jpg**</span><span class="sxs-lookup"><span data-stu-id="bb47b-138">This tells you that Blitline has recieved your request, it has put it in a processing queue, and when it has completed hello image will be available at: **https://s3.amazonaws.com/dev.blitline/2011110722/YOUR\_APP\_ID/CK3f0xBF_2bV6wf7gEZE8w.jpg**</span></span>

## <a name="how-toosave-an-image-tooyour-azure-storage-account"></a><span data-ttu-id="bb47b-139">如何 toosave 映像 tooyour Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="bb47b-139">How toosave an image tooyour Azure Storage account</span></span>
<span data-ttu-id="bb47b-140">如果您有 Azure 儲存體帳戶，您輕鬆地插入您的 Azure 容器有 Blitline 發送 hello 處理影像。</span><span class="sxs-lookup"><span data-stu-id="bb47b-140">If you have an Azure Storage account, you can easily have Blitline push hello processed images into your Azure container.</span></span> <span data-ttu-id="bb47b-141">藉由新增 「 azure_destination 」 您定義 hello 位置和要 Blitline toopush 權限。</span><span class="sxs-lookup"><span data-stu-id="bb47b-141">By adding an "azure_destination" you define hello location and permissions for Blitline toopush to.</span></span>

<span data-ttu-id="bb47b-142">下列是一個範例：</span><span class="sxs-lookup"><span data-stu-id="bb47b-142">Here is an example:</span></span>

    job : '{
      "application_id": "YOUR_APP_ID",
      "src" : "http://www.google.com/logos/2011/houdini11-hp.jpg",
         "functions" : [{
         "name": "blur",
         "save" : {
             "image_identifier" : "YOUR_IMAGE_IDENTIFIER",
             "azure_destination" : {
                 "account_name" : "YOUR_AZURE_CONTAINER_NAME",
                 "shared_access_signature" : "SAS_THAT_GIVES_BLITLINE_PERMISSION_TO_WRITE_THIS_OBJECT_TO_CONTAINER",
               }
           }
         }]
       }'


<span data-ttu-id="bb47b-143">填入與您自己的 hello CAPITALIZED 值，您可以送出此 JSON toohttp://api.blitline.com/job 並 hello"src 」 映像將使用模糊篩選處理然後推送至 tooyou Azure 的目的地。</span><span class="sxs-lookup"><span data-stu-id="bb47b-143">By filling in hello CAPITALIZED values with your own, you can submit this JSON toohttp://api.blitline.com/job and hello "src" image will be processed with a blur filter and then pushed tooyou Azure destination.</span></span>

### <a name="please-note"></a><span data-ttu-id="bb47b-144">請注意：</span><span class="sxs-lookup"><span data-stu-id="bb47b-144">Please note:</span></span>
<span data-ttu-id="bb47b-145">hello SAS 必須包含 hello 整個 SAS url，包括 hello hello 目的地檔案的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="bb47b-145">hello SAS must contain hello entire SAS url, including hello filename of hello destination file.</span></span>

<span data-ttu-id="bb47b-146">範例：</span><span class="sxs-lookup"><span data-stu-id="bb47b-146">Example:</span></span>

    http://blitline.blob.core.windows.net/sample/image.jpg?sr=b&sv=2012-02-12&st=2013-04-12T03%3A18%3A30Z&se=2013-04-12T04%3A18%3A30Z&sp=w&sig=Bte2hkkbwTT2sqlkkKLop2asByrE0sIfeesOwj7jNA5o%3D


<span data-ttu-id="bb47b-147">您也可以讀取 hello 的 Blitline 的 Azure 儲存體文件的最新版本[這裡](http://www.blitline.com/docs/azure_storage)。</span><span class="sxs-lookup"><span data-stu-id="bb47b-147">You can also read hello latest edition of Blitline's Azure Storage docs [here](http://www.blitline.com/docs/azure_storage).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bb47b-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bb47b-148">Next Steps</span></span>
<span data-ttu-id="bb47b-149">請造訪 blitline.com tooread 有關我們其他所有功能：</span><span class="sxs-lookup"><span data-stu-id="bb47b-149">Visit blitline.com tooread about all our other features:</span></span>

* <span data-ttu-id="bb47b-150">Blitline API 端點文件 <http://www.blitline.com/docs/api></span><span class="sxs-lookup"><span data-stu-id="bb47b-150">Blitline API Endpoint Docs <http://www.blitline.com/docs/api></span></span>
* <span data-ttu-id="bb47b-151">Blitline API 函式 <http://www.blitline.com/docs/functions></span><span class="sxs-lookup"><span data-stu-id="bb47b-151">Blitline API Functions <http://www.blitline.com/docs/functions></span></span>
* <span data-ttu-id="bb47b-152">Blitline API 範例 <http://www.blitline.com/docs/examples></span><span class="sxs-lookup"><span data-stu-id="bb47b-152">Blitline API Examples <http://www.blitline.com/docs/examples></span></span>
* <span data-ttu-id="bb47b-153">協力廠商 Nuget 程式庫 <http://nuget.org/packages/Blitline.Net></span><span class="sxs-lookup"><span data-stu-id="bb47b-153">Third Part Nuget Library <http://nuget.org/packages/Blitline.Net></span></span>

