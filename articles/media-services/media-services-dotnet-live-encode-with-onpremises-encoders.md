---
title: "如何使用 .NET 透過內部部署編碼器執行即時串流 | Microsoft Docs"
description: "本主題將說明如何使用 .NET 透過內部部署編碼器執行即時編碼。"
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
ms.openlocfilehash: 3ef6065f5b9e05e0ea5716548699943a2c877bc4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-perform-live-streaming-with-on-premises-encoders-using-net"></a><span data-ttu-id="dc06c-103">如何使用 .NET 透過內部部署編碼器執行即時視訊串流</span><span class="sxs-lookup"><span data-stu-id="dc06c-103">How to perform live streaming with on-premises encoders using .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="dc06c-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="dc06c-104">Portal</span></span>](media-services-portal-live-passthrough-get-started.md)
> * [<span data-ttu-id="dc06c-105">.NET</span><span class="sxs-lookup"><span data-stu-id="dc06c-105">.NET</span></span>](media-services-dotnet-live-encode-with-onpremises-encoders.md)
> * [<span data-ttu-id="dc06c-106">REST</span><span class="sxs-lookup"><span data-stu-id="dc06c-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> 

<span data-ttu-id="dc06c-107">本教學課程將逐步引導您使用 Azure 媒體服務 .NET SDK，建立針對即時通行傳遞設定的 **通道** 。</span><span class="sxs-lookup"><span data-stu-id="dc06c-107">This tutorial walks you through the steps of using the Azure Media Services .NET SDK to create a **Channel** that is configured for a pass-through delivery.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="dc06c-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="dc06c-108">Prerequisites</span></span>
<span data-ttu-id="dc06c-109">需要有下列項目，才能完成教學課程：</span><span class="sxs-lookup"><span data-stu-id="dc06c-109">The following are required to complete the tutorial:</span></span>

* <span data-ttu-id="dc06c-110">一個 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="dc06c-110">An Azure account.</span></span>
* <span data-ttu-id="dc06c-111">媒體服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="dc06c-111">A Media Services account.</span></span>    <span data-ttu-id="dc06c-112">若要建立媒體服務帳戶，請參閱[如何建立媒體服務帳戶](media-services-portal-create-account.md)。</span><span class="sxs-lookup"><span data-stu-id="dc06c-112">To create a Media Services account, see [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="dc06c-113">設定開發環境。</span><span class="sxs-lookup"><span data-stu-id="dc06c-113">Set up your dev environment.</span></span> <span data-ttu-id="dc06c-114">如需詳細資訊，請參閱 [設定環境](media-services-set-up-computer.md)。</span><span class="sxs-lookup"><span data-stu-id="dc06c-114">For more information, see [Set up your environment](media-services-set-up-computer.md).</span></span>
* <span data-ttu-id="dc06c-115">網路攝影機。</span><span class="sxs-lookup"><span data-stu-id="dc06c-115">A webcam.</span></span> <span data-ttu-id="dc06c-116">例如， [Telestream Wirecast 編碼器](http://www.telestream.net/wirecast/overview.htm)。</span><span class="sxs-lookup"><span data-stu-id="dc06c-116">For example, [Telestream Wirecast encoder](http://www.telestream.net/wirecast/overview.htm).</span></span>

<span data-ttu-id="dc06c-117">建議您先檢閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="dc06c-117">Recommended to review the following articles:</span></span>

* [<span data-ttu-id="dc06c-118">Azure 媒體服務 RTMP 支援和即時編碼器</span><span class="sxs-lookup"><span data-stu-id="dc06c-118">Azure Media Services RTMP Support and Live Encoders</span></span>](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/)
* [<span data-ttu-id="dc06c-119">使用會建立多位元速率串流的內部部署編碼器執行即時串流</span><span class="sxs-lookup"><span data-stu-id="dc06c-119">Live streaming with on-premises encoders that create multi-bitrate streams</span></span>](media-services-live-streaming-with-onprem-encoders.md)

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="dc06c-120">建立和設定 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="dc06c-120">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="dc06c-121">設定您的開發環境並在 app.config 檔案中填入連線資訊，如[使用 .NET 進行 Media Services 開發](media-services-dotnet-how-to-use.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="dc06c-121">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="example"></a><span data-ttu-id="dc06c-122">範例</span><span class="sxs-lookup"><span data-stu-id="dc06c-122">Example</span></span>
<span data-ttu-id="dc06c-123">下列程式碼範例示範如何完成下列工作：</span><span class="sxs-lookup"><span data-stu-id="dc06c-123">The following code example demonstrates how to achieve the following tasks:</span></span>

* <span data-ttu-id="dc06c-124">連線到媒體服務</span><span class="sxs-lookup"><span data-stu-id="dc06c-124">Connect to Media Services</span></span>
* <span data-ttu-id="dc06c-125">建立通道</span><span class="sxs-lookup"><span data-stu-id="dc06c-125">Create a channel</span></span>
* <span data-ttu-id="dc06c-126">更新通道</span><span class="sxs-lookup"><span data-stu-id="dc06c-126">Update the channel</span></span>
* <span data-ttu-id="dc06c-127">擷取通道的輸入端點。</span><span class="sxs-lookup"><span data-stu-id="dc06c-127">Retrieve the channel’s input endpoint.</span></span> <span data-ttu-id="dc06c-128">輸入端點應該提供給內部部署即時編碼器。</span><span class="sxs-lookup"><span data-stu-id="dc06c-128">The input endpoint should be provided to the on-premises live encoder.</span></span> <span data-ttu-id="dc06c-129">即時編碼器會將相機的訊號轉換為傳送到通道之輸入 (內嵌) 端點的資料流。</span><span class="sxs-lookup"><span data-stu-id="dc06c-129">The live encoder converts signals from the camera to streams that are sent to the channel’s input (ingest) endpoint.</span></span>
* <span data-ttu-id="dc06c-130">擷取通道的預覽端點</span><span class="sxs-lookup"><span data-stu-id="dc06c-130">Retrieve the channel’s preview endpoint</span></span>
* <span data-ttu-id="dc06c-131">建立並啟動程式</span><span class="sxs-lookup"><span data-stu-id="dc06c-131">Create and start a program</span></span>
* <span data-ttu-id="dc06c-132">建立存取程式所需的定位器</span><span class="sxs-lookup"><span data-stu-id="dc06c-132">Create a locator needed to access the program</span></span>
* <span data-ttu-id="dc06c-133">建立並啟動 StreamingEndpoint</span><span class="sxs-lookup"><span data-stu-id="dc06c-133">Create and start a StreamingEndpoint</span></span>
* <span data-ttu-id="dc06c-134">更新串流端點</span><span class="sxs-lookup"><span data-stu-id="dc06c-134">Update the streaming endpoint</span></span>
* <span data-ttu-id="dc06c-135">關閉資源</span><span class="sxs-lookup"><span data-stu-id="dc06c-135">Shut down resources</span></span>

>[!IMPORTANT]
><span data-ttu-id="dc06c-136">確定您想要串流內容的串流端點已處於 [執行中] 狀態。</span><span class="sxs-lookup"><span data-stu-id="dc06c-136">Make sure the streaming endpoint from which you want to stream content is in the **Running** state.</span></span> 
    
>[!NOTE]
><span data-ttu-id="dc06c-137">對於不同的 AMS 原則 (例如 Locator 原則或 ContentKeyAuthorizationPolicy) 有 1,000,000 個原則的限制。</span><span class="sxs-lookup"><span data-stu-id="dc06c-137">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="dc06c-138">如果您一律使用相同的日期 / 存取權限，例如，要長時間維持就地 (非上載原則) 的定位器原則，您應該使用相同的原則識別碼。</span><span class="sxs-lookup"><span data-stu-id="dc06c-138">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="dc06c-139">如需詳細資訊，請參閱 [這個](media-services-dotnet-manage-entities.md#limit-access-policies) 主題。</span><span class="sxs-lookup"><span data-stu-id="dc06c-139">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="dc06c-140">如需有關如何設定即時編碼器的詳細資訊，請參閱 [Azure 媒體服務 RTMP 支援和即時編碼器](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/)。</span><span class="sxs-lookup"><span data-stu-id="dc06c-140">For information on how to configure a live encoder, see [Azure Media Services RTMP Support and Live Encoders](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/).</span></span>

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

        // Read values from the App.config file.
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

            // Set the Live Encoder to point to the channel's input endpoint:
            string ingestUrl = channel.Input.Endpoints.FirstOrDefault().Url.ToString();

            // Use the previewEndpoint to preview and verify
            // that the input from the encoder is actually reaching the Channel.
            string previewEndpoint = channel.Preview.Endpoints.FirstOrDefault().Url.ToString();

            IProgram program = CreateAndStartProgram(channel);
            ILocator locator = CreateLocatorForAsset(program.Asset, program.ArchiveWindowLength);
            IStreamingEndpoint streamingEndpoint = CreateAndStartStreamingEndpoint(false);

            // Once you are done streaming, clean up your resources.
            Cleanup(streamingEndpoint, channel);
        }

        public static IChannel CreateAndStartChannel()
        {
            //If you want to change the Smooth fragments to HLS segment ratio, you would set the ChannelCreationOptions’s Output property.

            IChannel channel = _context.Channels.Create(
            new ChannelCreationOptions
            {
            Name = ChannelName,
            Input = CreateChannelInput(),
            Preview = CreateChannelPreview()
            });

            //Starting and stopping Channels can take some time to execute. To determine the state of operations after calling Start or Stop, query the IChannel.State .

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
                    // will allow access to IP addresses.
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
                    // will allow access to IP addresses.
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

            // Create a Program on the Channel. You can have multiple Programs that overlap or are sequential;
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

## <a name="next-step"></a><span data-ttu-id="dc06c-141">下一步</span><span class="sxs-lookup"><span data-stu-id="dc06c-141">Next Step</span></span>
<span data-ttu-id="dc06c-142">檢閱媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="dc06c-142">Review Media Services learning paths</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="dc06c-143">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="dc06c-143">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

