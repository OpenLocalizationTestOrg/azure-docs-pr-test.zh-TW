---
title: "aaaHow tooperform 即時資料流與內部部署編碼器使用.NET |Microsoft 文件"
description: "本主題說明如何 toouse.NET tooperform 即時編碼與在內部部署編碼器。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 15908152-d23c-4d55-906a-3bfd74927db5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 07/18/2017
ms.author: cenkdin;juliako
ms.openlocfilehash: 332582c9f925f8b9270929b3fa8140fce010bbf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-live-streaming-with-on-premises-encoders-using-net"></a><span data-ttu-id="e2749-103">如何 tooperform 即時資料流與內部部署編碼器使用的.NET</span><span class="sxs-lookup"><span data-stu-id="e2749-103">How tooperform live streaming with on-premises encoders using .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e2749-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="e2749-104">Portal</span></span>](media-services-portal-live-passthrough-get-started.md)
> * [<span data-ttu-id="e2749-105">.NET</span><span class="sxs-lookup"><span data-stu-id="e2749-105">.NET</span></span>](media-services-dotnet-live-encode-with-onpremises-encoders.md)
> * [<span data-ttu-id="e2749-106">REST</span><span class="sxs-lookup"><span data-stu-id="e2749-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> 

<span data-ttu-id="e2749-107">本教學課程會引導您逐步使用 hello Azure Media Services.NET SDK toocreate hello**通道**針對傳遞的傳遞設定。</span><span class="sxs-lookup"><span data-stu-id="e2749-107">This tutorial walks you through hello steps of using hello Azure Media Services .NET SDK toocreate a **Channel** that is configured for a pass-through delivery.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="e2749-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="e2749-108">Prerequisites</span></span>
<span data-ttu-id="e2749-109">hello 下面是必要的 toocomplete hello 教學課程：</span><span class="sxs-lookup"><span data-stu-id="e2749-109">hello following are required toocomplete hello tutorial:</span></span>

* <span data-ttu-id="e2749-110">一個 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="e2749-110">An Azure account.</span></span>
* <span data-ttu-id="e2749-111">媒體服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="e2749-111">A Media Services account.</span></span>    <span data-ttu-id="e2749-112">toocreate Media Services 帳戶，請參閱[如何 tooCreate Media Services 帳戶](media-services-portal-create-account.md)。</span><span class="sxs-lookup"><span data-stu-id="e2749-112">toocreate a Media Services account, see [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="e2749-113">設定開發環境。</span><span class="sxs-lookup"><span data-stu-id="e2749-113">Set up your dev environment.</span></span> <span data-ttu-id="e2749-114">如需詳細資訊，請參閱 [設定環境](media-services-set-up-computer.md)。</span><span class="sxs-lookup"><span data-stu-id="e2749-114">For more information, see [Set up your environment](media-services-set-up-computer.md).</span></span>
* <span data-ttu-id="e2749-115">網路攝影機。</span><span class="sxs-lookup"><span data-stu-id="e2749-115">A webcam.</span></span> <span data-ttu-id="e2749-116">例如， [Telestream Wirecast 編碼器](http://www.telestream.net/wirecast/overview.htm)。</span><span class="sxs-lookup"><span data-stu-id="e2749-116">For example, [Telestream Wirecast encoder](http://www.telestream.net/wirecast/overview.htm).</span></span>

<span data-ttu-id="e2749-117">下列文件的建議的 tooreview hello:</span><span class="sxs-lookup"><span data-stu-id="e2749-117">Recommended tooreview hello following articles:</span></span>

* [<span data-ttu-id="e2749-118">Azure 媒體服務 RTMP 支援和即時編碼器</span><span class="sxs-lookup"><span data-stu-id="e2749-118">Azure Media Services RTMP Support and Live Encoders</span></span>](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/)
* [<span data-ttu-id="e2749-119">使用會建立多位元速率串流的內部部署編碼器執行即時串流</span><span class="sxs-lookup"><span data-stu-id="e2749-119">Live streaming with on-premises encoders that create multi-bitrate streams</span></span>](media-services-live-streaming-with-onprem-encoders.md)

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="e2749-120">建立和設定 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="e2749-120">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="e2749-121">設定您的開發環境，並填入 hello 與連接資訊的 app.config 檔案中所述[與.NET 的 Media Services 開發](media-services-dotnet-how-to-use.md)。</span><span class="sxs-lookup"><span data-stu-id="e2749-121">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="example"></a><span data-ttu-id="e2749-122">範例</span><span class="sxs-lookup"><span data-stu-id="e2749-122">Example</span></span>
<span data-ttu-id="e2749-123">hello，下列程式碼範例示範如何 tooachieve hello 下列工作：</span><span class="sxs-lookup"><span data-stu-id="e2749-123">hello following code example demonstrates how tooachieve hello following tasks:</span></span>

* <span data-ttu-id="e2749-124">TooMedia 服務連接</span><span class="sxs-lookup"><span data-stu-id="e2749-124">Connect tooMedia Services</span></span>
* <span data-ttu-id="e2749-125">建立通道</span><span class="sxs-lookup"><span data-stu-id="e2749-125">Create a channel</span></span>
* <span data-ttu-id="e2749-126">更新 hello 頻道</span><span class="sxs-lookup"><span data-stu-id="e2749-126">Update hello channel</span></span>
* <span data-ttu-id="e2749-127">擷取 hello 通道輸入的端點。</span><span class="sxs-lookup"><span data-stu-id="e2749-127">Retrieve hello channel’s input endpoint.</span></span> <span data-ttu-id="e2749-128">toohello 內部部署即時編碼器應提供 hello 輸入的端點。</span><span class="sxs-lookup"><span data-stu-id="e2749-128">hello input endpoint should be provided toohello on-premises live encoder.</span></span> <span data-ttu-id="e2749-129">從傳送 toohello 瑎堀熁檓 hello 相機 toostreams hello 即時編碼器將訊號 （內嵌） 端點。</span><span class="sxs-lookup"><span data-stu-id="e2749-129">hello live encoder converts signals from hello camera toostreams that are sent toohello channel’s input (ingest) endpoint.</span></span>
* <span data-ttu-id="e2749-130">擷取 hello 通道預覽端點</span><span class="sxs-lookup"><span data-stu-id="e2749-130">Retrieve hello channel’s preview endpoint</span></span>
* <span data-ttu-id="e2749-131">建立並啟動程式</span><span class="sxs-lookup"><span data-stu-id="e2749-131">Create and start a program</span></span>
* <span data-ttu-id="e2749-132">建立定位器需要 tooaccess hello 程式</span><span class="sxs-lookup"><span data-stu-id="e2749-132">Create a locator needed tooaccess hello program</span></span>
* <span data-ttu-id="e2749-133">建立並啟動 StreamingEndpoint</span><span class="sxs-lookup"><span data-stu-id="e2749-133">Create and start a StreamingEndpoint</span></span>
* <span data-ttu-id="e2749-134">更新串流端點的 hello</span><span class="sxs-lookup"><span data-stu-id="e2749-134">Update hello streaming endpoint</span></span>
* <span data-ttu-id="e2749-135">關閉資源</span><span class="sxs-lookup"><span data-stu-id="e2749-135">Shut down resources</span></span>

>[!IMPORTANT]
><span data-ttu-id="e2749-136">請確定 hello 串流的端點要從中 toostream 內容處於 hello**執行**狀態。</span><span class="sxs-lookup"><span data-stu-id="e2749-136">Make sure hello streaming endpoint from which you want toostream content is in hello **Running** state.</span></span> 
    
>[!NOTE]
><span data-ttu-id="e2749-137">對於不同的 AMS 原則 (例如 Locator 原則或 ContentKeyAuthorizationPolicy) 有 1,000,000 個原則的限制。</span><span class="sxs-lookup"><span data-stu-id="e2749-137">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="e2749-138">您應該使用 hello 如果一律使用相同的原則識別碼 hello 相同天 / 存取權限，例如，原則會就地預定的 tooremain 長時間 （非上載原則） 的定位器。</span><span class="sxs-lookup"><span data-stu-id="e2749-138">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="e2749-139">如需詳細資訊，請參閱 [這個](media-services-dotnet-manage-entities.md#limit-access-policies) 主題。</span><span class="sxs-lookup"><span data-stu-id="e2749-139">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="e2749-140">如需詳細資訊 tooconfigure 即時編碼程式，請參閱[Azure Media Services RTMP 支援和即時編碼程式](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/)。</span><span class="sxs-lookup"><span data-stu-id="e2749-140">For information on how tooconfigure a live encoder, see [Azure Media Services RTMP Support and Live Encoders](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/).</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.Linq;
    using System.Net;
    using System.Security.Cryptography;
    using Microsoft.WindowsAzure.MediaServices.Client;

    namespace AMSLiveTest
    {
        class Program
        {
        private const string StreamingEndpointName = "streamingendpoint001";
        private const string ChannelName = "channel001";
        private const string AssetlName = "asset001";
        private const string ProgramlName = "program001";

        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static CloudMediaContext _context = null;

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            IChannel channel = CreateAndStartChannel();

            // Set hello Live Encoder toopoint toohello channel's input endpoint:
            string ingestUrl = channel.Input.Endpoints.FirstOrDefault().Url.ToString();

            // Use hello previewEndpoint toopreview and verify
            // that hello input from hello encoder is actually reaching hello Channel.
            string previewEndpoint = channel.Preview.Endpoints.FirstOrDefault().Url.ToString();

            IProgram program = CreateAndStartProgram(channel);
            ILocator locator = CreateLocatorForAsset(program.Asset, program.ArchiveWindowLength);
            IStreamingEndpoint streamingEndpoint = CreateAndStartStreamingEndpoint(false);

            // Once you are done streaming, clean up your resources.
            Cleanup(streamingEndpoint, channel);
        }

        public static IChannel CreateAndStartChannel()
        {
            //If you want toochange hello Smooth fragments tooHLS segment ratio, you would set hello ChannelCreationOptions’s Output property.

            IChannel channel = _context.Channels.Create(
            new ChannelCreationOptions
            {
            Name = ChannelName,
            Input = CreateChannelInput(),
            Preview = CreateChannelPreview()
            });

            //Starting and stopping Channels can take some time tooexecute. toodetermine hello state of operations after calling Start or Stop, query hello IChannel.State .

            channel.Start();

            return channel;
        }

        private static ChannelInput CreateChannelInput()
        {
            return new ChannelInput
            {
            StreamingProtocol = StreamingProtocol.RTMP,
            AccessControl = new ChannelAccessControl
            {
                IPAllowList = new List<IPRange>
                    {
                    new IPRange
                    {
                    Name = "TestChannelInput001",
                    // Setting 0.0.0.0 for Address and 0 for SubnetPrefixLength
                    // will allow access tooIP addresses.
                    Address = IPAddress.Parse("0.0.0.0"),
                    SubnetPrefixLength = 0
                    }
                }
            }
            };
        }

        private static ChannelPreview CreateChannelPreview()
        {
            return new ChannelPreview
            {
            AccessControl = new ChannelAccessControl
            {
                IPAllowList = new List<IPRange>
                {
                    new IPRange
                    {
                    Name = "TestChannelPreview001",
                    // Setting 0.0.0.0 for Address and 0 for SubnetPrefixLength
                    // will allow access tooIP addresses.
                    Address = IPAddress.Parse("0.0.0.0"),
                    SubnetPrefixLength = 0
                    }
                }
            }
            };
        }

        public static void UpdateCrossSiteAccessPoliciesForChannel(IChannel channel)
        {
            var clientPolicy =
            @"<?xml version=""1.0"" encoding=""utf-8""?>
            <access-policy>
                <cross-domain-access>
                <policy>
                    <allow-from http-request-headers=""*"" http-methods=""*"">
                    <domain uri=""*""/>
                    </allow-from>
                    <grant-to>
                       <resource path=""/"" include-subpaths=""true""/>
                    </grant-to>
                </policy>
                </cross-domain-access>
            </access-policy>";

            var xdomainPolicy =
            @"<?xml version=""1.0"" ?>
            <cross-domain-policy>
                <allow-access-from domain=""*"" />
            </cross-domain-policy>";

            channel.CrossSiteAccessPolicies.ClientAccessPolicy = clientPolicy;
            channel.CrossSiteAccessPolicies.CrossDomainPolicy = xdomainPolicy;

            channel.Update();
        }

        public static IProgram CreateAndStartProgram(IChannel channel)
        {
            IAsset asset = _context.Assets.Create(AssetlName, AssetCreationOptions.None);

            // Create a Program on hello Channel. You can have multiple Programs that overlap or are sequential;
            // however each Program must have a unique name within your Media Services account.
            IProgram program = channel.Programs.Create(ProgramlName, TimeSpan.FromHours(3), asset.Id);
            program.Start();

            return program;
        }

        public static ILocator CreateLocatorForAsset(IAsset asset, TimeSpan ArchiveWindowLength)
        {
            // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.            

            var locator = _context.Locators.CreateLocator
            (
                LocatorType.OnDemandOrigin,
                asset,
                _context.AccessPolicies.Create
                (
                "Live Stream Policy",
                ArchiveWindowLength,
                AccessPermissions.Read
                )
            );

            return locator;
        }

        public static IStreamingEndpoint CreateAndStartStreamingEndpoint(bool createNew)
        {
            IStreamingEndpoint streamingEndpoint = null;
            if (createNew)
            {
            var options = new StreamingEndpointCreationOptions
            {
                Name = StreamingEndpointName,
                ScaleUnits = 1,
                AccessControl = GetAccessControl(),
                CacheControl = GetCacheControl()
            };

            streamingEndpoint = _context.StreamingEndpoints.Create(options);
            }
            else
            {
            streamingEndpoint = _context.StreamingEndpoints.FirstOrDefault();
            }


            if (streamingEndpoint.State == StreamingEndpointState.Stopped)
            streamingEndpoint.Start();

            return streamingEndpoint;
        }

        private static StreamingEndpointAccessControl GetAccessControl()
        {
            return new StreamingEndpointAccessControl
            {
            IPAllowList = new List<IPRange>
                {
                new IPRange
                {
                    Name = "Allow all",
                    Address = IPAddress.Parse("0.0.0.0"),
                    SubnetPrefixLength = 0
                }
                },

            AkamaiSignatureHeaderAuthenticationKeyList = new List<AkamaiSignatureHeaderAuthenticationKey>
                {
                new AkamaiSignatureHeaderAuthenticationKey
                {
                    Identifier = "My key",
                    Expiration = DateTime.UtcNow + TimeSpan.FromDays(365),
                    Base64Key = Convert.ToBase64String(GenerateRandomBytes(16))
                }
                }
            };
        }

        private static byte[] GenerateRandomBytes(int length)
        {
            var bytes = new byte[length];
            using (var rng = new RNGCryptoServiceProvider())
            {
            rng.GetBytes(bytes);
            }

            return bytes;
        }

        private static StreamingEndpointCacheControl GetCacheControl()
        {
            return new StreamingEndpointCacheControl
            {
            MaxAge = TimeSpan.FromSeconds(1000)
            };
        }

        public static void UpdateCrossSiteAccessPoliciesForStreamingEndpoint(IStreamingEndpoint streamingEndpoint)
        {
            var clientPolicy =
            @"<?xml version=""1.0"" encoding=""utf-8""?>
            <access-policy>
                <cross-domain-access>
                <policy>
                    <allow-from http-request-headers=""*"" http-methods=""*"">
                    <domain uri=""*""/>
                    </allow-from>
                    <grant-to>
                       <resource path=""/"" include-subpaths=""true""/>
                    </grant-to>
                </policy>
                </cross-domain-access>
            </access-policy>";

            var xdomainPolicy =
            @"<?xml version=""1.0"" ?>
            <cross-domain-policy>
                <allow-access-from domain=""*"" />
            </cross-domain-policy>";

            streamingEndpoint.CrossSiteAccessPolicies.ClientAccessPolicy = clientPolicy;
            streamingEndpoint.CrossSiteAccessPolicies.CrossDomainPolicy = xdomainPolicy;

            streamingEndpoint.Update();
        }

        public static void Cleanup(IStreamingEndpoint streamingEndpoint,
                        IChannel channel)
        {
            if (streamingEndpoint != null)
            {
            streamingEndpoint.Stop();
            if(streamingEndpoint.Name != "default")
                streamingEndpoint.Delete();
            }

            IAsset asset;
            if (channel != null)
            {

            foreach (var program in channel.Programs)
            {
                asset = _context.Assets.Where(se => se.Id == program.AssetId)
                            .FirstOrDefault();

                program.Stop();
                program.Delete();

                if (asset != null)
                {
                foreach (var l in asset.Locators)
                    l.Delete();

                asset.Delete();
                }
            }

            channel.Stop();
            channel.Delete();
            }
        }
        }
    }

## <a name="next-step"></a><span data-ttu-id="e2749-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e2749-141">Next Step</span></span>
<span data-ttu-id="e2749-142">檢閱媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="e2749-142">Review Media Services learning paths</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e2749-143">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="e2749-143">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

