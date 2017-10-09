---
title: "aaaPolling 長時間執行的作業 |Microsoft 文件"
description: "本主題說明如何 toopoll 長時間執行的作業。"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 9a68c4b1-6159-42fe-9439-a3661a90ae03
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: f8315a5ddbe484d794c3e2164e47dd9e70521671
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="delivering-live-streaming-with-azure-media-services"></a>利用 Azure 媒體服務提供即時資料流

## <a name="overview"></a>概觀

Microsoft Azure Media Services 提供的 Api，以傳送要求 tooMedia Services toostart 作業 (例如： 建立、 啟動、 停止或刪除通道)。 這些作業屬於長時間執行的作業。

hello Media Services.NET SDK 提供傳送嗨要求，並等候 hello 作業 toocomplete (就內部而言，應用程式開發介面特定間隔輪詢作業進度的 hello) 的 Api。 例如，當您呼叫通道。Start （），hello 方法會傳回 hello 通道啟動後。 您也可以使用 hello 非同步版本： 等候通道。StartAsync() (以工作為基礎的非同步模式的相關資訊，請參閱[點選](https://msdn.microsoft.com/library/hh873175\(v=vs.110\).aspx))。 應用程式開發介面傳送的作業要求和 hello 作業完成之前輪詢 hello 狀態稱為 「 輪詢方法 」。 建議使用這些方法 （尤其是 hello 非同步版本） 的豐富型用戶端應用程式及/或可設定狀態的服務。

沒有應用程式無法等待長時間執行的 http 要求，而想 toopoll hello 作業進度，以手動方式。 常見的範例是與無狀態的 web 服務互動的瀏覽器： hello 瀏覽器要求 toocreate 通道、 hello web 服務會起始長時間執行的作業和傳回 hello 作業 ID toohello 瀏覽器時。 hello 瀏覽器無法再要求 hello web 服務 tooget hello 作業狀態 hello id。 hello Media Services.NET SDK 提供可用於此案例中的 Api。 這些 API 稱為「非輪詢方法」。
hello 「 非輪詢方法 」 具有下列命名模式的 hello： 傳送*OperationName*作業 (例如，SendCreateOperation)。 傳送*OperationName*作業方法會傳回 hello **IOperation**物件; hello 傳回的物件包含可能是使用的 tootrack hello 作業的資訊。 傳送嗨*OperationName*OperationAsync 方法會傳回**工作<IOperation>**。

目前，hello 遵循類別支援非輪詢方法：**通道**， **StreamingEndpoint**，和**程式**。

hello 作業狀態，使用 hello toopoll **GetOperation**方法上 hello **OperationBaseCollection**類別。 使用下列間隔 toocheck hello 作業狀態的 hello： 針對**通道**和**StreamingEndpoint**作業，請使用 30 秒; 對於**程式**作業，請使用 10秒數。

## <a name="create-and-configure-a-visual-studio-project"></a>建立和設定 Visual Studio 專案

設定您的開發環境，並填入 hello 與連接資訊的 app.config 檔案中所述[與.NET 的 Media Services 開發](media-services-dotnet-how-to-use.md)。

## <a name="example"></a>範例

hello 下列範例會定義一種類別稱為**ChannelOperations**。 此類別定義可能是 Web 服務類別定義的起始點。 為了簡單起見，hello 下列範例會使用 hello 方法的非同步版本。

hello 範例也會顯示 hello 用戶端如何使用這個類別。

### <a name="channeloperations-class-definition"></a>ChannelOperations class definition

    using Microsoft.WindowsAzure.MediaServices.Client;
    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.Net;

    /// <summary> 
    /// hello ChannelOperations class only implements 
    /// hello Channel’s creation operation. 
    /// </summary> 
    public class ChannelOperations
    {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        // Field for service context.
        private static CloudMediaContext _context = null;

        public ChannelOperations()
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);
        }

        /// <summary>  
        /// Initiates hello creation of a new channel.  
        /// </summary>  
        /// <param name="channelName">Name toobe given toohello new channel</param>  
        /// <returns>  
        /// Operation Id for hello long running operation being executed by Media Services. 
        /// Use this operation Id toopoll for hello channel creation status. 
        /// </returns> 
        public string StartChannelCreation(string channelName)
        {
            var operation = _context.Channels.SendCreateOperation(
                new ChannelCreationOptions
                {
                    Name = channelName,
                    Input = CreateChannelInput(),
                    Preview = CreateChannelPreview(),
                    Output = CreateChannelOutput()
                });

            return operation.Id;
        }

        /// <summary> 
        /// Checks if hello operation has been completed. 
        /// If hello operation succeeded, hello created channel Id is returned in hello out parameter.
        /// </summary> 
        /// <param name="operationId">hello operation Id.</param> 
        /// <param name="channel">
        /// If hello operation succeeded, 
        /// hello created channel Id is returned in hello out parameter.</param>
        /// <returns>Returns false if hello operation is still in progress; otherwise, true.</returns> 
        public bool IsCompleted(string operationId, out string channelId)
        {
            IOperation operation = _context.Operations.GetOperation(operationId);
            bool completed = false;

            channelId = null;

            switch (operation.State)
            {
                case OperationState.Failed:
                    // Handle hello failure. 
                    // For example, throw an exception. 
                    // Use hello following information in hello exception: operationId, operation.ErrorMessage.
                    break;
                case OperationState.Succeeded:
                    completed = true;
                    channelId = operation.TargetEntityId;
                    break;
                case OperationState.InProgress:
                    completed = false;
                    break;
            }
            return completed;
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
                                Address = IPAddress.Parse("0.0.0.0"),
                                SubnetPrefixLength = 0
                            }
                        }
                }
            };
        }

        private static ChannelOutput CreateChannelOutput()
        {
            return new ChannelOutput
            {
                Hls = new ChannelOutputHls { FragmentsPerSegment = 1 }
            };
        }
    }

### <a name="hello-client-code"></a>hello 用戶端程式碼
    ChannelOperations channelOperations = new ChannelOperations();
    string opId = channelOperations.StartChannelCreation("MyChannel001");

    string channelId = null;
    bool isCompleted = false;

    while (isCompleted == false)
    {
        System.Threading.Thread.Sleep(TimeSpan.FromSeconds(30));
        isCompleted = channelOperations.IsCompleted(opId, out channelId);
    }

    // If we got here, we should have hello newly created channel id.
    Console.WriteLine(channelId);



## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

