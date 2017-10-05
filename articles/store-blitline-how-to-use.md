---
title: "如何使用 Blitline 進行影像處理 - Azure 功能指南"
description: "了解如何使用 Blitline 服務處理 Azure 應用程式內的影像。"
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
ms.openlocfilehash: 1d90599e028b3407a513b04b878e3aefc39928a2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-blitline-with-azure-and-azure-storage"></a><span data-ttu-id="918c0-103">如何使用搭配 Azure 和 Azure 儲存體的 Blitline</span><span class="sxs-lookup"><span data-stu-id="918c0-103">How to use Blitline with Azure and Azure Storage</span></span>
<span data-ttu-id="918c0-104">本指南將說明如何存取 Blitline 服務，以及如何將工作提交至 Blitline。</span><span class="sxs-lookup"><span data-stu-id="918c0-104">This guide will explain how to access Blitline services and how to submit jobs to Blitline.</span></span>

## <a name="what-is-blitline"></a><span data-ttu-id="918c0-105">什麼是 Blitline？</span><span class="sxs-lookup"><span data-stu-id="918c0-105">What is Blitline?</span></span>
<span data-ttu-id="918c0-106">Blitline 是雲端影像處理服務，可提供企業級的影像處理，而價格卻只有自我建置的數分之一。</span><span class="sxs-lookup"><span data-stu-id="918c0-106">Blitline is a cloud-based image processing service that provides enterprise level image processing at a fraction of the price that it would cost to build it yourself.</span></span>

<span data-ttu-id="918c0-107">事實上，影像處理一再重複出現，通常需要從頭開始重新建置每個網站。</span><span class="sxs-lookup"><span data-stu-id="918c0-107">The fact is that image processing has been done over and over again, usually rebuilt from the ground up for each and every website.</span></span> <span data-ttu-id="918c0-108">我們了解這個情況，那是因為我們已經建立了上百萬次。</span><span class="sxs-lookup"><span data-stu-id="918c0-108">We realize this because we’ve built them a million times too.</span></span> <span data-ttu-id="918c0-109">有一天，我們決定或許是替所有人執行此動作的時候了。</span><span class="sxs-lookup"><span data-stu-id="918c0-109">One day we decided that perhaps it‘s time we just do it for everyone.</span></span> <span data-ttu-id="918c0-110">我們知道如何做、如何做得快以及做得有效率，並同時減輕每個人的工作。</span><span class="sxs-lookup"><span data-stu-id="918c0-110">We know how to do it, to do it fast and efficiently, and save everyone work in the meantime.</span></span>

<span data-ttu-id="918c0-111">如需詳細資訊，請參閱 [http://www.blitline.com](http://www.blitline.com)(英文)。</span><span class="sxs-lookup"><span data-stu-id="918c0-111">For more information, see [http://www.blitline.com](http://www.blitline.com).</span></span>

## <a name="what-blitline-is-not"></a><span data-ttu-id="918c0-112">Blitline 不是什麼...</span><span class="sxs-lookup"><span data-stu-id="918c0-112">What Blitline is NOT...</span></span>
<span data-ttu-id="918c0-113">若要釐清 Blitline 有什麼功能，在繼續之前，找出 Blitline 沒有什麼功能通常比較容易。</span><span class="sxs-lookup"><span data-stu-id="918c0-113">To clarify what Blitline is useful for, it is often easier to identify what Blitline does NOT do before moving forward.</span></span>

* <span data-ttu-id="918c0-114">Blitline 沒有上傳影像的 HTML Widget。</span><span class="sxs-lookup"><span data-stu-id="918c0-114">Blitline does NOT have HTML widgets to upload images.</span></span> <span data-ttu-id="918c0-115">您必須要有公開可用的影像，或 Blitline 可用來存取的限制權限。</span><span class="sxs-lookup"><span data-stu-id="918c0-115">You must have images available publicly or with restricted permissions available for Blitline to reach.</span></span>
* <span data-ttu-id="918c0-116">Blitline 不會執行即時影像處理，如 Aviary.com</span><span class="sxs-lookup"><span data-stu-id="918c0-116">Blitline does NOT do live image processing, like Aviary.com</span></span>
* <span data-ttu-id="918c0-117">Blitline 不接受影像上傳，您無法將影像直接推送至 Blitline。</span><span class="sxs-lookup"><span data-stu-id="918c0-117">Blitline does NOT accept image uploads, you cannot push your images to Blitline directly.</span></span> <span data-ttu-id="918c0-118">您必須將影像推送至 Azure 儲存體或其他 Blitline 支援的位置，然後通知 Blitline 取得這些影像的位置。</span><span class="sxs-lookup"><span data-stu-id="918c0-118">You must push them to Azure Storage or other places Blitline supports and then tell Blitline where to go get them.</span></span>
* <span data-ttu-id="918c0-119">Blitline 可大量平行處理，但無法執行任何同步處理。</span><span class="sxs-lookup"><span data-stu-id="918c0-119">Blitline is massively parallel and does NOT do any synchronous processing.</span></span> <span data-ttu-id="918c0-120">這表示您必須提供 postback_url 給我們，我們會在處理完成時通知您。</span><span class="sxs-lookup"><span data-stu-id="918c0-120">Meaning you must give us a postback_url and we can tell you when we are done processing.</span></span>

## <a name="create-a-blitline-account"></a><span data-ttu-id="918c0-121">建立 Blitline 帳戶</span><span class="sxs-lookup"><span data-stu-id="918c0-121">Create a Blitline account</span></span>
[!INCLUDE [blitline-signup](../includes/blitline-signup.md)]

## <a name="how-to-create-a-blitline-job"></a><span data-ttu-id="918c0-122">如何建立 Blitline 工作</span><span class="sxs-lookup"><span data-stu-id="918c0-122">How to create a Blitline job</span></span>
<span data-ttu-id="918c0-123">Blitline 使用 JSON 定義您要對影像採取的動作。</span><span class="sxs-lookup"><span data-stu-id="918c0-123">Blitline uses JSON to define the actions you want to take on an image.</span></span> <span data-ttu-id="918c0-124">此 JSON 是由幾個簡單欄位組合而成。</span><span class="sxs-lookup"><span data-stu-id="918c0-124">This JSON is composed of a few simple fields.</span></span>

<span data-ttu-id="918c0-125">下列是個最簡單範例：</span><span class="sxs-lookup"><span data-stu-id="918c0-125">The simplest example is as follows:</span></span>

        json : '{
       "application_id": "MY_APP_ID",
       "src" : "http://cdn.blitline.com/filters/boys.jpeg",
       "functions" : [ {
           "name": "resize_to_fit",
           "params" : { "width": 240, "height": 140 },
           "save" : { "image_identifier" : "external_sample_1" }
       } ]
    }'

<span data-ttu-id="918c0-126">在此，我們要求 JSON 準備一個 "src" 影像 "...boys.jpeg"，然後將該影像大小調整為 240x140。</span><span class="sxs-lookup"><span data-stu-id="918c0-126">Here we have JSON that will take a "src" image "...boys.jpeg" and then resize that image to 240x140.</span></span>

<span data-ttu-id="918c0-127">您可以在 Azure 上的 [連接資訊] 或 [管理] 索引標籤中找到應用程式識別碼的資訊。</span><span class="sxs-lookup"><span data-stu-id="918c0-127">The Application ID is something you can find in your **CONNECTION INFO** or **MANAGE** tab on Azure.</span></span> <span data-ttu-id="918c0-128">應用程式識別碼是可讓您在 Blitline 上執行工作的密碼識別碼。</span><span class="sxs-lookup"><span data-stu-id="918c0-128">It is your secret identifier that allows you to run jobs on Blitline.</span></span>

<span data-ttu-id="918c0-129">"save" 參數可識別有關處理完影像時，您想要放置該影像的位置資訊。</span><span class="sxs-lookup"><span data-stu-id="918c0-129">The "save" parameter identifies information about where you want to put the image once we have processed it.</span></span> <span data-ttu-id="918c0-130">在這個簡單的案例中，我們尚未定義一個位置。</span><span class="sxs-lookup"><span data-stu-id="918c0-130">In this trivial case, we haven't defined one.</span></span> <span data-ttu-id="918c0-131">如果沒有定義位置，Blitline 會將它儲存在本機 (並暫時地) 的唯一雲端位置。</span><span class="sxs-lookup"><span data-stu-id="918c0-131">If no location is defined Blitline will store it locally (and temporarily) at a unique cloud location.</span></span> <span data-ttu-id="918c0-132">建立 Blitline 時，您將能夠從 Blitline 所傳回的 JSON 取得該位置。</span><span class="sxs-lookup"><span data-stu-id="918c0-132">You will be able to get that location from the JSON returned by Blitline when you make the Blitline.</span></span> <span data-ttu-id="918c0-133">"image" 識別碼為必要欄位，並會在要識別此特定儲存影像時傳回。</span><span class="sxs-lookup"><span data-stu-id="918c0-133">The "image" identifier is required and is returned to you when to identify this particular saved image.</span></span>

<span data-ttu-id="918c0-134">您可以在下列連結中找到有關我們可支援的更多「函式」相關資訊：<http://www.blitline.com/docs/functions></span><span class="sxs-lookup"><span data-stu-id="918c0-134">You can find more information about the *functions* we support here: <http://www.blitline.com/docs/functions></span></span>

<span data-ttu-id="918c0-135">您也可以在下列連結中找到有關工作選項的相關文件：<http://www.blitline.com/docs/api></span><span class="sxs-lookup"><span data-stu-id="918c0-135">You can also find documentation about the job options here: <http://www.blitline.com/docs/api></span></span>

<span data-ttu-id="918c0-136">在有了 JSON 之後，您唯一需要做的動作是將它 **POST** 至 `http://api.blitline.com/job`</span><span class="sxs-lookup"><span data-stu-id="918c0-136">Once you have your JSON all you need to do is **POST** it to `http://api.blitline.com/job`</span></span>

<span data-ttu-id="918c0-137">您將取回如下所示的 JSON：</span><span class="sxs-lookup"><span data-stu-id="918c0-137">You will get JSON back that looks something like this:</span></span>

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


<span data-ttu-id="918c0-138">這代表 Blitline 已收到您的要求，它已將您的要求置入處理佇列，且當它完成影像時的影像位置： **https://s3.amazonaws.com/dev.blitline/2011110722/YOUR\_APP\_ID/CK3f0xBF_2bV6wf7gEZE8w.jpg**</span><span class="sxs-lookup"><span data-stu-id="918c0-138">This tells you that Blitline has recieved your request, it has put it in a processing queue, and when it has completed the image will be available at: **https://s3.amazonaws.com/dev.blitline/2011110722/YOUR\_APP\_ID/CK3f0xBF_2bV6wf7gEZE8w.jpg**</span></span>

## <a name="how-to-save-an-image-to-your-azure-storage-account"></a><span data-ttu-id="918c0-139">如何將影像儲存至您的 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="918c0-139">How to save an image to your Azure Storage account</span></span>
<span data-ttu-id="918c0-140">如果您有 Azure 儲存體帳戶，您可以輕易地要求 Blitline 將已處理的影像推送到 Azure 容器。</span><span class="sxs-lookup"><span data-stu-id="918c0-140">If you have an Azure Storage account, you can easily have Blitline push the processed images into your Azure container.</span></span> <span data-ttu-id="918c0-141">透過新增 "azure_destination"，您可以定義 Blitline 要推送的位置和權限。</span><span class="sxs-lookup"><span data-stu-id="918c0-141">By adding an "azure_destination" you define the location and permissions for Blitline to push to.</span></span>

<span data-ttu-id="918c0-142">下列是一個範例：</span><span class="sxs-lookup"><span data-stu-id="918c0-142">Here is an example:</span></span>

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


<span data-ttu-id="918c0-143">透過靠您自己填入大寫值，您可以將此 JSON 提交至 http://api.blitline.com/job，並對 "src" 影像採用模糊濾鏡的處理，然後推送至 Azure 目的地。</span><span class="sxs-lookup"><span data-stu-id="918c0-143">By filling in the CAPITALIZED values with your own, you can submit this JSON to http://api.blitline.com/job and the "src" image will be processed with a blur filter and then pushed to you Azure destination.</span></span>

### <a name="please-note"></a><span data-ttu-id="918c0-144">請注意：</span><span class="sxs-lookup"><span data-stu-id="918c0-144">Please note:</span></span>
<span data-ttu-id="918c0-145">SAS 必須包含整個 SAS URL，包括目的地檔案的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="918c0-145">The SAS must contain the entire SAS url, including the filename of the destination file.</span></span>

<span data-ttu-id="918c0-146">範例：</span><span class="sxs-lookup"><span data-stu-id="918c0-146">Example:</span></span>

    http://blitline.blob.core.windows.net/sample/image.jpg?sr=b&sv=2012-02-12&st=2013-04-12T03%3A18%3A30Z&se=2013-04-12T04%3A18%3A30Z&sp=w&sig=Bte2hkkbwTT2sqlkkKLop2asByrE0sIfeesOwj7jNA5o%3D


<span data-ttu-id="918c0-147">您也可以參閱 [此處](http://www.blitline.com/docs/azure_storage)(英文) 的最新版本 Blitline Azure 儲存體文件。</span><span class="sxs-lookup"><span data-stu-id="918c0-147">You can also read the latest edition of Blitline's Azure Storage docs [here](http://www.blitline.com/docs/azure_storage).</span></span>

## <a name="next-steps"></a><span data-ttu-id="918c0-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="918c0-148">Next Steps</span></span>
<span data-ttu-id="918c0-149">請造訪 blitline.com 以閱讀所有其他功能：</span><span class="sxs-lookup"><span data-stu-id="918c0-149">Visit blitline.com to read about all our other features:</span></span>

* <span data-ttu-id="918c0-150">Blitline API 端點文件 <http://www.blitline.com/docs/api></span><span class="sxs-lookup"><span data-stu-id="918c0-150">Blitline API Endpoint Docs <http://www.blitline.com/docs/api></span></span>
* <span data-ttu-id="918c0-151">Blitline API 函式 <http://www.blitline.com/docs/functions></span><span class="sxs-lookup"><span data-stu-id="918c0-151">Blitline API Functions <http://www.blitline.com/docs/functions></span></span>
* <span data-ttu-id="918c0-152">Blitline API 範例 <http://www.blitline.com/docs/examples></span><span class="sxs-lookup"><span data-stu-id="918c0-152">Blitline API Examples <http://www.blitline.com/docs/examples></span></span>
* <span data-ttu-id="918c0-153">協力廠商 Nuget 程式庫 <http://nuget.org/packages/Blitline.Net></span><span class="sxs-lookup"><span data-stu-id="918c0-153">Third Part Nuget Library <http://nuget.org/packages/Blitline.Net></span></span>

