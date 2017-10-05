---
title: "使用 .NET 設定 Azure 媒體服務遙測 | Microsoft Docs"
description: "本文示範如何透過 .NET SDK 使用 Azure 媒體服務遙測。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: f8f55e37-0714-49ea-bf4a-e6c1319bec44
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 1d857f3d062d8d1b15c64fa4b8c3e27ad6c2247e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="configuring-azure-media-services-telemetry-with-net"></a><span data-ttu-id="c6348-103">使用 .NET 設定 Azure 媒體服務遙測</span><span class="sxs-lookup"><span data-stu-id="c6348-103">Configuring Azure Media Services telemetry with .NET</span></span>

<span data-ttu-id="c6348-104">本主題說明您使用 .NET SDK 設定 Azure 媒體服務 (AMS) 遙測時可能採取的一般步驟。</span><span class="sxs-lookup"><span data-stu-id="c6348-104">This topic describes general steps that you might take when configuring the Azure Media Services (AMS) telemetry using .NET SDK.</span></span> 

>[!NOTE]
><span data-ttu-id="c6348-105">如需什麼是 AMS 遙測及如何取用的詳細說明，請參閱[概觀](media-services-telemetry-overview.md)主題。</span><span class="sxs-lookup"><span data-stu-id="c6348-105">For the detailed explanation of what is AMS telemetry and how to consume it, see the [overview](media-services-telemetry-overview.md) topic.</span></span>

<span data-ttu-id="c6348-106">您可以使用下列其中一個方法取用遙測資料︰</span><span class="sxs-lookup"><span data-stu-id="c6348-106">You can consume telemetry data in one of the following ways:</span></span>

- <span data-ttu-id="c6348-107">直接從 Azure 表格儲存體 (例如使用儲存體 SDK) 中讀取資料。</span><span class="sxs-lookup"><span data-stu-id="c6348-107">Read data directly from Azure Table Storage (e.g. using the Storage SDK).</span></span> <span data-ttu-id="c6348-108">如需遙測儲存體資料表的說明，請參閱[這個](https://msdn.microsoft.com/library/mt742089.aspx)主題中的**取用遙測資訊**。</span><span class="sxs-lookup"><span data-stu-id="c6348-108">For the description of telemetry storage tables, see the **Consuming telemetry information** in [this](https://msdn.microsoft.com/library/mt742089.aspx) topic.</span></span>

<span data-ttu-id="c6348-109">或</span><span class="sxs-lookup"><span data-stu-id="c6348-109">Or</span></span>

- <span data-ttu-id="c6348-110">使用媒體服務 .NET SDK 中的支援讀取儲存體資料。</span><span class="sxs-lookup"><span data-stu-id="c6348-110">Use the support in the Media Services .NET SDK for reading storage data.</span></span> <span data-ttu-id="c6348-111">本主題示範如何為指定的 AMS 帳戶啟用遙測，以及如何使用 Azure 媒體服務 .NET SDK 查詢度量。</span><span class="sxs-lookup"><span data-stu-id="c6348-111">This topic shows how to enable telemetry for the specified AMS account and how to query the metrics using the Azure Media Services .NET SDK.</span></span>  

## <a name="configuring-telemetry-for-a-media-services-account"></a><span data-ttu-id="c6348-112">設定媒體服務帳戶的遙測</span><span class="sxs-lookup"><span data-stu-id="c6348-112">Configuring telemetry for a Media Services account</span></span>

<span data-ttu-id="c6348-113">若要啟用遙測，您需要執行下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="c6348-113">The following steps are needed to enable telemetry:</span></span>

- <span data-ttu-id="c6348-114">取得媒體服務帳戶附加之儲存體帳戶的認證。</span><span class="sxs-lookup"><span data-stu-id="c6348-114">Get the credentials of the storage account attached to the Media Services account.</span></span> 
- <span data-ttu-id="c6348-115">建立 **EndPointType** 設定為 **AzureTable** 且 endPontAddress 指向儲存體資料表的通知端點。</span><span class="sxs-lookup"><span data-stu-id="c6348-115">Create a Notification Endpoint with **EndPointType** set to **AzureTable** and endPointAddress pointing to the storage table.</span></span>

        INotificationEndPoint notificationEndPoint = 
                      _context.NotificationEndPoints.Create("monitoring", 
                      NotificationEndPointType.AzureTable,
                      "https://" + _mediaServicesStorageAccountName + ".table.core.windows.net/");

- <span data-ttu-id="c6348-116">針對要監視的服務建立監視組態設定。</span><span class="sxs-lookup"><span data-stu-id="c6348-116">Create a monitoring configuration settings for the services you want to monitor.</span></span> <span data-ttu-id="c6348-117">系統最多只允許一個監視組態設定。</span><span class="sxs-lookup"><span data-stu-id="c6348-117">No more than one monitoring configuration settings is allowed.</span></span> 
  
        IMonitoringConfiguration monitoringConfiguration = _context.MonitoringConfigurations.Create(notificationEndPoint.Id,
            new List<ComponentMonitoringSetting>()
            {
                new ComponentMonitoringSetting(MonitoringComponent.Channel, MonitoringLevel.Normal),
                new ComponentMonitoringSetting(MonitoringComponent.StreamingEndpoint, MonitoringLevel.Normal)
            });

## <a name="consuming-telemetry-information"></a><span data-ttu-id="c6348-118">取用遙測資訊</span><span class="sxs-lookup"><span data-stu-id="c6348-118">Consuming telemetry information</span></span>

<span data-ttu-id="c6348-119">如需取用遙測資訊的相關資訊，請參閱[這個](media-services-telemetry-overview.md)主題。</span><span class="sxs-lookup"><span data-stu-id="c6348-119">For information about consuming telemetry information, see [this](media-services-telemetry-overview.md) topic.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="c6348-120">建立和設定 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="c6348-120">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="c6348-121">設定您的開發環境並在 app.config 檔案中填入連線資訊，如[使用 .NET 進行 Media Services 開發](media-services-dotnet-how-to-use.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="c6348-121">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

2. <span data-ttu-id="c6348-122">將下列項目新增至 app.config 檔案中定義的 **appSettings**：</span><span class="sxs-lookup"><span data-stu-id="c6348-122">Add the following element to **appSettings** defined in your app.config file:</span></span>

    <add key="StorageAccountName" value="storage_name" />
 
## <a name="example"></a><span data-ttu-id="c6348-123">範例</span><span class="sxs-lookup"><span data-stu-id="c6348-123">Example</span></span>  
    
<span data-ttu-id="c6348-124">下列範例示範如何為指定的 AMS 帳戶啟用遙測，以及如何使用 Azure 媒體服務 .NET SDK 查詢度量。</span><span class="sxs-lookup"><span data-stu-id="c6348-124">The following example shows how to enable telemetry for the specified AMS account and how to query the metrics using the Azure Media Services .NET SDK.</span></span>  

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;

    namespace AMSMetrics
    {
        class Program
        {
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static readonly string _mediaServicesStorageAccountName =
            ConfigurationManager.AppSettings["StorageAccountName"];

        // Field for service context.
        private static CloudMediaContext _context = null;

        private static IStreamingEndpoint _streamingEndpoint = null;
        private static IChannel _channel = null;

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            _streamingEndpoint = _context.StreamingEndpoints.FirstOrDefault();
            _channel = _context.Channels.FirstOrDefault();

            var monitoringConfigurations = _context.MonitoringConfigurations;
            IMonitoringConfiguration monitoringConfiguration = null;

            // No more than one monitoring configuration settings is allowed.
            if (monitoringConfigurations.ToArray().Length != 0)
            {
            monitoringConfiguration = _context.MonitoringConfigurations.FirstOrDefault();
            }
            else
            {
            INotificationEndPoint notificationEndPoint =
                      _context.NotificationEndPoints.Create("monitoring",
                      NotificationEndPointType.AzureTable, GetTableEndPoint());

            monitoringConfiguration = _context.MonitoringConfigurations.Create(notificationEndPoint.Id,
                new List<ComponentMonitoringSetting>()
                {
                    new ComponentMonitoringSetting(MonitoringComponent.Channel, MonitoringLevel.Normal),
                    new ComponentMonitoringSetting(MonitoringComponent.StreamingEndpoint, MonitoringLevel.Normal)

                });
            }

            //Print metrics for a Streaming Endpoint.
            PrintStreamingEndpointMetrics();

            Console.ReadLine();
        }

        private static string GetTableEndPoint()
        {
            return "https://" + _mediaServicesStorageAccountName + ".table.core.windows.net/";
        }

        private static void PrintStreamingEndpointMetrics()
        {
            Console.WriteLine(string.Format("Telemetry for streaming endpoint '{0}'", _streamingEndpoint.Name));

            DateTime timerangeEnd = DateTime.UtcNow;
            DateTime timerangeStart = DateTime.UtcNow.AddHours(-5);

            // Get some streaming endpoint metrics.
            var telemetry = _streamingEndpoint.GetTelemetry();

            var res = telemetry.GetStreamingEndpointRequestLogs(timerangeStart, timerangeEnd);

            Console.Title = "Streaming endpoint metrics:";

            foreach (var log in res)
            {
            Console.WriteLine("AccountId: {0}", log.AccountId);
            Console.WriteLine("BytesSent: {0}", log.BytesSent);
            Console.WriteLine("EndToEndLatency: {0}", log.EndToEndLatency);
            Console.WriteLine("HostName: {0}", log.HostName);
            Console.WriteLine("ObservedTime: {0}", log.ObservedTime);
            Console.WriteLine("PartitionKey: {0}", log.PartitionKey);
            Console.WriteLine("RequestCount: {0}", log.RequestCount);
            Console.WriteLine("ResultCode: {0}", log.ResultCode);
            Console.WriteLine("RowKey: {0}", log.RowKey);
            Console.WriteLine("ServerLatency: {0}", log.ServerLatency);
            Console.WriteLine("StatusCode: {0}", log.StatusCode);
            Console.WriteLine("StreamingEndpointId: {0}", log.StreamingEndpointId);
            Console.WriteLine();
            }

            Console.WriteLine();
        }

        private static void PrintChannelMetrics()
        {
            if (_channel == null)
            {
            Console.WriteLine("There are no channels in this AMS account");
            return;
            }

            Console.WriteLine(string.Format("Telemetry for channel '{0}'", _channel.Name));

            DateTime timerangeEnd = DateTime.UtcNow; 
            DateTime timerangeStart = DateTime.UtcNow.AddHours(-5);

            // Get some channel metrics.
            var telemetry = _channel.GetTelemetry();

            var channelMetrics = telemetry.GetChannelHeartbeats(timerangeStart, timerangeEnd);

            // Print the channel metrics.
            Console.WriteLine("Channel metrics:");

            foreach (var channelHeartbeat in channelMetrics.OrderBy(x => x.ObservedTime))
            {
            Console.WriteLine(
                "    Observed time: {0}, Last timestamp: {1}, Incoming bitrate: {2}",
                channelHeartbeat.ObservedTime,
                channelHeartbeat.LastTimestamp,
                channelHeartbeat.IncomingBitrate);
            }

            Console.WriteLine();
        }
        }
    }


## <a name="next-steps"></a><span data-ttu-id="c6348-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c6348-125">Next steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c6348-126">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="c6348-126">Provide feedback</span></span>

[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
