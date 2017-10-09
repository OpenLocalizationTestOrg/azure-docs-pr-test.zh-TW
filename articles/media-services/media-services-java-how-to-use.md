---
title: "在需要使用 Java 傳遞內容入門 aaaGet |Microsoft 文件"
description: "本教學課程會引導您實作與使用 Java 的 Azure 媒體服務 (AMS) 應用程式的基本 Video-on-Demand (VoD) 內容傳遞服務的 hello 步驟。"
services: media-services
documentationcenter: java
author: juliako
manager: cfowler
editor: 
ms.assetid: b884bd61-dbdb-42ea-b170-8fb02e7fded7
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: get-started-article
ms.date: 01/10/2017
ms.author: juliako
ms.openlocfilehash: b13eb88e35fb0d7a1ec1a213293080bad8aa1806
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-java"></a><span data-ttu-id="ceb34-103">使用 Java 傳遞點播內容入門</span><span class="sxs-lookup"><span data-stu-id="ceb34-103">Get started with delivering content on demand using Java</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="ceb34-104">本教學課程會引導您實作與使用 Java 的 Azure 媒體服務 (AMS) 應用程式的基本 Video-on-Demand (VoD) 內容傳遞服務的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="ceb34-104">This tutorial walks you through hello steps of implementing a basic Video-on-Demand (VoD) content delivery service with Azure Media Services (AMS) application using Java.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ceb34-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="ceb34-105">Prerequisites</span></span>

<span data-ttu-id="ceb34-106">hello 下面是必要的 toocomplete hello 教學課程：</span><span class="sxs-lookup"><span data-stu-id="ceb34-106">hello following are required toocomplete hello tutorial:</span></span>

* <span data-ttu-id="ceb34-107">一個 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ceb34-107">An Azure account.</span></span> <span data-ttu-id="ceb34-108">如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="ceb34-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="ceb34-109">媒體服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="ceb34-109">A Media Services account.</span></span> <span data-ttu-id="ceb34-110">toocreate Media Services 帳戶，請參閱[如何 tooCreate Media Services 帳戶](media-services-portal-create-account.md)。</span><span class="sxs-lookup"><span data-stu-id="ceb34-110">toocreate a Media Services account, see [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="ceb34-111">hello Azure Libraries for Java，您可以從 hello 安裝[Azure Java 開發人員中心][Azure Java Developer Center]。</span><span class="sxs-lookup"><span data-stu-id="ceb34-111">hello Azure Libraries for Java, which you can install from hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

## <a name="how-to-use-media-services-with-java"></a><span data-ttu-id="ceb34-112">如何：搭配使用媒體服務和 Java</span><span class="sxs-lookup"><span data-stu-id="ceb34-112">How to: Use Media Services with Java</span></span>

>[!NOTE]
><span data-ttu-id="ceb34-113">AMS 帳戶建立時**預設**串流端點就會加入 tooyour 帳戶 hello**已停止**狀態。</span><span class="sxs-lookup"><span data-stu-id="ceb34-113">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="ceb34-114">串流處理您的內容，並採取利用動態封裝和動態加密，toostart hello 串流端點，您想要從中 toostream 內容已經在 hello toobe**執行**狀態。</span><span class="sxs-lookup"><span data-stu-id="ceb34-114">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 

>[!NOTE]
><span data-ttu-id="ceb34-115">對於不同的 AMS 原則 (例如 Locator 原則或 ContentKeyAuthorizationPolicy) 有 1,000,000 個原則的限制。</span><span class="sxs-lookup"><span data-stu-id="ceb34-115">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="ceb34-116">您應該使用 hello 如果一律使用相同的原則識別碼 hello 相同天 / 存取權限，例如，原則會就地預定的 tooremain 長時間 （非上載原則） 的定位器。</span><span class="sxs-lookup"><span data-stu-id="ceb34-116">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="ceb34-117">如需詳細資訊，請參閱 [這個](media-services-dotnet-manage-entities.md#limit-access-policies) 主題。</span><span class="sxs-lookup"><span data-stu-id="ceb34-117">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="ceb34-118">hello 下列程式碼說明如何 toocreate 資產上, 傳媒體檔案 toohello 資產、 執行工作與工作 tootransform hello 的資產，並建立定位器 toostream 視訊。</span><span class="sxs-lookup"><span data-stu-id="ceb34-118">hello following code shows how toocreate an asset, upload a media file toohello asset, run a job with a task tootransform hello asset, and create a locator toostream your video.</span></span>

<span data-ttu-id="ceb34-119">您需要建立 Media Services 帳戶 tooset 才能使用這個程式碼。</span><span class="sxs-lookup"><span data-stu-id="ceb34-119">You need tooset up a Media Services account before using this code.</span></span> <span data-ttu-id="ceb34-120">設定帳戶的詳細資訊，請參閱[如何 tooCreate Media Services 帳戶](media-services-portal-create-account.md)。</span><span class="sxs-lookup"><span data-stu-id="ceb34-120">For information about setting up an account, see [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>

<span data-ttu-id="ceb34-121">替換為您的 hello 'clientId' 和 'Clientid' 變數的值。</span><span class="sxs-lookup"><span data-stu-id="ceb34-121">Substitute your values for hello 'clientId' and 'clientSecret' variables.</span></span> <span data-ttu-id="ceb34-122">hello 程式碼也依賴本機儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="ceb34-122">hello code also relies on a locally stored file.</span></span> <span data-ttu-id="ceb34-123">您將需要您自己的檔案 toouse tooprovide。</span><span class="sxs-lookup"><span data-stu-id="ceb34-123">You'll need tooprovide your own file toouse.</span></span>

    import java.io.*;
    import java.security.NoSuchAlgorithmException;
    import java.util.EnumSet;

    import com.microsoft.windowsazure.Configuration;
    import com.microsoft.windowsazure.exception.ServiceException;
    import com.microsoft.windowsazure.services.media.MediaConfiguration;
    import com.microsoft.windowsazure.services.media.MediaContract;
    import com.microsoft.windowsazure.services.media.MediaService;
    import com.microsoft.windowsazure.services.media.WritableBlobContainerContract;
    import com.microsoft.windowsazure.services.media.models.AccessPolicy;
    import com.microsoft.windowsazure.services.media.models.AccessPolicyInfo;
    import com.microsoft.windowsazure.services.media.models.AccessPolicyPermission;
    import com.microsoft.windowsazure.services.media.models.Asset;
    import com.microsoft.windowsazure.services.media.models.AssetFile;
    import com.microsoft.windowsazure.services.media.models.AssetFileInfo;
    import com.microsoft.windowsazure.services.media.models.AssetInfo;
    import com.microsoft.windowsazure.services.media.models.Job;
    import com.microsoft.windowsazure.services.media.models.JobInfo;
    import com.microsoft.windowsazure.services.media.models.JobState;
    import com.microsoft.windowsazure.services.media.models.ListResult;
    import com.microsoft.windowsazure.services.media.models.Locator;
    import com.microsoft.windowsazure.services.media.models.LocatorInfo;
    import com.microsoft.windowsazure.services.media.models.LocatorType;
    import com.microsoft.windowsazure.services.media.models.MediaProcessor;
    import com.microsoft.windowsazure.services.media.models.MediaProcessorInfo;
    import com.microsoft.windowsazure.services.media.models.Task;

    public class HelloMediaServices
    {
        // Media Services account credentials configuration
        private static String mediaServiceUri = "https://media.windows.net/API/";
        private static String oAuthUri = "https://wamsprodglobal001acs.accesscontrol.windows.net/v2/OAuth2-13";
        private static String clientId = "account name";
        private static String clientSecret = "account key";
        private static String scope = "urn:WindowsAzureMediaServices";
        private static MediaContract mediaService;

        // Encoder configuration
        private static String preferedEncoder = "Media Encoder Standard";
        private static String encodingPreset = "Adaptive Streaming";

        public static void main(String[] args)
        {

            try {
                // Set up hello MediaContract object toocall into hello Media Services account
                Configuration configuration = MediaConfiguration.configureWithOAuthAuthentication(
                mediaServiceUri, oAuthUri, clientId, clientSecret, scope);
                mediaService = MediaService.create(configuration);


                // Upload a local file tooan Asset
                AssetInfo uploadAsset = uploadFileAndCreateAsset("BigBuckBunny.mp4");
                System.out.println("Uploaded Asset Id: " + uploadAsset.getId());


                // Transform hello Asset
                AssetInfo encodedAsset = encode(uploadAsset);
                System.out.println("Encoded Asset Id: " + encodedAsset.getId());

                // Create hello Streaming Origin Locator
                String url = getStreamingOriginLocator(encodedAsset);

                System.out.println("Origin Locator URL: " + url);
                System.out.println("Sample completed!");

            } catch (ServiceException se) {
                System.out.println("ServiceException encountered.");
                System.out.println(se.toString());
            } catch (Exception e) {
                System.out.println("Exception encountered.");
                System.out.println(e.toString());
            }

        }

        private static AssetInfo uploadFileAndCreateAsset(String fileName)
            throws ServiceException, FileNotFoundException, NoSuchAlgorithmException {

            WritableBlobContainerContract uploader;
            AssetInfo resultAsset;
            AccessPolicyInfo uploadAccessPolicy;
            LocatorInfo uploadLocator = null;

            // Create an Asset
            resultAsset = mediaService.create(Asset.create().setName(fileName).setAlternateId("altId"));
            System.out.println("Created Asset " + fileName);

            // Create an AccessPolicy that provides Write access for 15 minutes
            uploadAccessPolicy = mediaService
                .create(AccessPolicy.create("uploadAccessPolicy", 15.0, EnumSet.of(AccessPolicyPermission.WRITE)));

            // Create a Locator using hello AccessPolicy and Asset
            uploadLocator = mediaService
                .create(Locator.create(uploadAccessPolicy.getId(), resultAsset.getId(), LocatorType.SAS));

            // Create hello Blob Writer using hello Locator
            uploader = mediaService.createBlobWriter(uploadLocator);

            File file = new File("BigBuckBunny.mp4"); 

            // hello local file that will be uploaded tooyour Media Services account
            InputStream input = new FileInputStream(file);

            System.out.println("Uploading " + fileName);

            // Upload hello local file toohello asset
            uploader.createBlockBlob(fileName, input);

            // Inform Media Services about hello uploaded files
            mediaService.action(AssetFile.createFileInfos(resultAsset.getId()));
            System.out.println("Uploaded Asset File " + fileName);

            mediaService.delete(Locator.delete(uploadLocator.getId()));
            mediaService.delete(AccessPolicy.delete(uploadAccessPolicy.getId()));

            return resultAsset;
        }

        // Create a Job that contains a Task tootransform hello Asset
        private static AssetInfo encode(AssetInfo assetToEncode)
            throws ServiceException, InterruptedException {

            // Retrieve hello list of Media Processors that match hello name
            ListResult<MediaProcessorInfo> mediaProcessors = mediaService
                            .list(MediaProcessor.list().set("$filter", String.format("Name eq '%s'", preferedEncoder)));

            // Use hello latest version of hello Media Processor
            MediaProcessorInfo mediaProcessor = null;
            for (MediaProcessorInfo info : mediaProcessors) {
                if (null == mediaProcessor || info.getVersion().compareTo(mediaProcessor.getVersion()) > 0) {
                    mediaProcessor = info;
                }
            }

            System.out.println("Using Media Processor: " + mediaProcessor.getName() + " " + mediaProcessor.getVersion());

            // Create a task with hello specified Media Processor
            String outputAssetName = String.format("%s as %s", assetToEncode.getName(), encodingPreset);
            String taskXml = "<taskBody><inputAsset>JobInputAsset(0)</inputAsset>"
                    + "<outputAsset assetCreationOptions=\"0\"" // AssetCreationOptions.None
                    + " assetName=\"" + outputAssetName + "\">JobOutputAsset(0)</outputAsset></taskBody>";

            Task.CreateBatchOperation task = Task.create(mediaProcessor.getId(), taskXml)
                    .setConfiguration(encodingPreset).setName("Encoding");

            // Create hello Job; this automatically schedules and runs it.
            Job.Creator jobCreator = Job.create()
                    .setName(String.format("Encoding %s too%s", assetToEncode.getName(), encodingPreset))
                    .addInputMediaAsset(assetToEncode.getId()).setPriority(2).addTaskCreator(task);
            JobInfo job = mediaService.create(jobCreator);

            String jobId = job.getId();
            System.out.println("Created Job with Id: " + jobId);

            // Check toosee if hello Job has completed
            checkJobStatus(jobId);
            // Done with hello Job

            // Retrieve hello output Asset
            ListResult<AssetInfo> outputAssets = mediaService.list(Asset.list(job.getOutputAssetsLink()));
            return outputAssets.get(0);
        }


        public static String getStreamingOriginLocator(AssetInfo asset) throws ServiceException {
            // Get hello .ISM AssetFile
            ListResult<AssetFileInfo> assetFiles = mediaService.list(AssetFile.list(asset.getAssetFilesLink()));
            AssetFileInfo streamingAssetFile = null;
            for (AssetFileInfo file : assetFiles) {
                if (file.getName().toLowerCase().endsWith(".ism")) {
                    streamingAssetFile = file;
                    break;
                }
            }

            AccessPolicyInfo originAccessPolicy;
            LocatorInfo originLocator = null;

            // Create a 30-day readonly AccessPolicy
            double durationInMinutes = 60 * 24 * 30;
            originAccessPolicy = mediaService.create(
                    AccessPolicy.create("Streaming policy", durationInMinutes, EnumSet.of(AccessPolicyPermission.READ)));

            // Create a Locator using hello AccessPolicy and Asset
            originLocator = mediaService
                    .create(Locator.create(originAccessPolicy.getId(), asset.getId(), LocatorType.OnDemandOrigin));

            // Create a Smooth Streaming base URL
            return originLocator.getPath() + streamingAssetFile.getName() + "/manifest";
        }

        private static void checkJobStatus(String jobId) throws InterruptedException, ServiceException {
            boolean done = false;
            JobState jobState = null;
            while (!done) {
                // Sleep for 5 seconds
                Thread.sleep(5000);

                // Query hello updated Job state
                jobState = mediaService.get(Job.get(jobId)).getState();
                System.out.println("Job state: " + jobState);

                if (jobState == JobState.Finished || jobState == JobState.Canceled || jobState == JobState.Error) {
                    done = true;
                }
            }
        }

    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="ceb34-124">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="ceb34-124">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ceb34-125">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="ceb34-125">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="additional-resources"></a><span data-ttu-id="ceb34-126">其他資源</span><span class="sxs-lookup"><span data-stu-id="ceb34-126">Additional Resources</span></span>
<span data-ttu-id="ceb34-127">如需媒體服務 Javadoc 文件，請參閱 [Azure Libraries for Java 文件][Azure Libraries for Java documentation]。</span><span class="sxs-lookup"><span data-stu-id="ceb34-127">For Media Services Javadoc documentation, see [Azure Libraries for Java documentation][Azure Libraries for Java documentation].</span></span>

<!-- URLs. -->

[Azure Java Developer Center]: http://azure.microsoft.com/develop/java/
[Azure Libraries for Java documentation]: http://dl.windowsazure.com/javadoc/
[Media Services Client Development]: http://msdn.microsoft.com/library/windowsazure/dn223283.aspx
