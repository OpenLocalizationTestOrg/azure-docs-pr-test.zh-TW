---
title: "aaaWhat 為 hello Azure WebJobs SDK"
description: "簡介 toohello Azure WebJobs SDK。 說明哪些 hello SDK，一般的案例很有用，而且程式碼範例。"
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 8281267b-572b-4b14-a328-6704493ea682
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: efac7a75c3b68a6a6601fb298f2ccac9bd71709d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-azure-webjobs-sdk"></a>Hello Azure WebJobs SDK 是什麼
## <a id="overview"></a>概觀
這篇文章會說明什麼 hello WebJobs SDK 是的會檢閱一些常見的案例很有用，並提供如何使用它在程式碼中的概觀。

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

[WebJobs](websites-webjobs-resources.md)程式或指令碼在 hello 是 toorun 可讓您的 Azure 應用程式服務的功能為 web 應用程式、 應用程式開發介面應用程式或行動裝置應用程式相同的內容。 hello 目的 hello [WebJobs SDK](websites-webjobs-resources.md) toosimplify hello 程式碼，您可以執行的 WebJob，例如映像處理、 佇列的處理、 RSS 彙總、 檔案維護的一般工作為撰寫，且傳送電子郵件。 hello WebJobs SDK 有內建的功能，使用 Azure 儲存體和 Service Bus、 工作排程和處理錯誤，以及許多其他常見的案例。 此外，其設計目的是 toobe 可延伸。 hello [WebJobs SDK 是開放原始碼](https://github.com/Azure/azure-webjobs-sdk/)，而且沒有[擴充功能的開放原始碼儲存機制](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview)。

hello WebJobs SDK 包含下列元件的 hello:

* **NuGet 封裝**。 您加入 tooa Visual Studio 主控台應用程式專案的 NuGet 套件提供一種架構，而將 WebJobs SDK 屬性與方法的程式碼使用。
* **儀表板**。 Hello WebJobs SDK 的一部分包含在 Azure 應用程式服務，並提供豐富的監視和診斷使用 hello NuGet 封裝的程式。 您不需要 toowrite 程式碼 toouse 這些監視和診斷功能。

## <a id="scenarios"></a>案例
以下是一些典型的案例，您可以更輕鬆地處理以 hello Azure WebJobs SDK:

* 影像處理或其他需要大量 CPU 的工作。 網站的共通的功能是 hello 能力 tooupload 影像或視訊。 通常您之後想要 toomanipulate hello 內容上傳，但當您這麼做時，您不想 toomake hello 使用者等候。
* 佇列處理。 與後端服務的 web 前端 toocommunicate 的常用方式是 toouse 佇列。 當 hello 網站需要 tooget 工作完成時，它會推送到佇列的訊息。 後端服務會從 hello 佇列提取訊息，並沒有 hello 工作。 您可以使用映像處理佇列： 例如，hello 使用者上傳的檔案數目之後，將 hello 檔案名稱以收取 hello 後端處理的佇列訊息 toobe。 或者，您可以使用佇列 tooimprove 網站回應速度。 例如，而不是直接寫入 tooa SQL database，撰寫 tooa 佇列，告訴您完成時，並讓 hello 後端服務控制代碼高延遲關聯式資料庫工作的 hello 使用者。 如需佇列處理的映像程序的範例，請參閱 hello [WebJobs SDK 快速入門教學課程](websites-dotnet-webjobs-sdk-get-started.md)。
* RSS 彙總。 如果您有站台維護的 RSS 摘要清單，您無法提取所有 hello 發行項的背景處理序中的 hello 摘要。
* 檔案維護，例如彙總或清除記錄檔案。  您可能必須建立數個站台或不同的記錄檔時間範圍以您想 toocombine 中排序 toorun 分析作業在其上。 或者，您可能想 tooschedule 舊的記錄檔的工作 toorun 每週 tooclean。
* 輸入 Azure 資料表。 您可能已儲存的檔案和 blob，並想 tooparse 它們 hello 資料並儲存在資料表。 hello 輸入函式可能會寫入大量資料列 （在某些情況下包含數百萬），並 hello WebJobs SDK，讓可能 tooimplement 這項功能容易。 hello SDK 也提供即時監視進度指標，例如 hello 寫入 hello 資料表中的資料列數目。
* 其他長時間執行工作，例如要在背景執行緒、 toorun[傳送電子郵件](https://github.com/victorhurdugaci/AzureWebJobsSamples/tree/master/SendEmailOnFailure)。 
* 您想依排程，例如執行備份作業每晚 toorun 任何工作。

在許多案例中，您可能想 tooscale web 應用程式 toorun 上多個 Vm，就會同時執行多個 WebJobs。 在某些情況下，這可能導致 hello 相同資料進行處理多次，但這不是 hello 的問題使用內建 hello 的佇列、 blob 和 Service Bus WebJobs SDK 的觸發程序時。 hello SDK 可確保您的函式將會一次處理的每個訊息或 blob。

hello WebJobs SDK 也可讓您輕鬆 toohandle 常見的錯誤處理案例。 您可以設定警示通知 toosend 當函式失敗，並使函式會自動取消，如果它未在指定的時間限制內完成，您可以設定逾時。

## <a id="code"></a> 程式碼範例
hello 處理可搭配 Azure 儲存體的一般工作的程式碼很簡單。 在主控台應用程式的`Main`方法建立`JobHost`協調 hello 的物件呼叫的 toomethods 您撰寫。 hello WebJobs SDK 架構知道當您的方法，及哪些參數值 toouse 根據 hello WebJobs SDK toocall 屬性中加以使用。 hello SDK 提供*觸發程序*旗標會指定什麼條件會造成呼叫，hello 函式 toobe 和*繫結器*旗標會指定如何執行和跳離方法參數的 tooget 資訊。

例如，hello [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)屬性就會導致佇列接收訊息時，如果 hello 訊息格式的位元組陣列或自訂型別為 JSON，hello 訊息就會自動還原序列化時呼叫的函式 toobe。 hello [BlobTrigger](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)屬性觸發程序，每次在 Azure 儲存體帳戶中建立新的 blob。

下列是個簡單程式，可用來輪詢佇列並為收到的每則佇列訊息建立 Blob：

        public static void Main()
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

        public static void ProcessQueueMessage([QueueTrigger("webjobsqueue")] string inputText, 
            [Blob("containername/blobname")]TextWriter writer)
        {
            writer.WriteLine(inputText);
        }

hello`JobHost`物件是一組背景函式的容器。 hello`JobHost`物件監視 hello 函式、 監看觸發這些事件和觸發程序事件發生時執行 hello 函式。 您呼叫`JobHost`方法 tooindicate 是否要在 hello 容器程序 toorun hello 目前的執行緒或背景執行緒。 在 hello 範例 hello`RunAndBlock`方法 hello 程序會持續執行 hello 目前執行緒上。

因為 hello`ProcessQueueMessage`在此範例中的方法有`QueueTrigger`屬性，hello 觸發程序該函式是 hello 訊息接收的新佇列。 hello`JobHost`物件會監看 hello 指定佇列 (在此範例中為"webjobsqueue 」) 上的新佇列訊息，並找到一個物件，它會呼叫`ProcessQueueMessage`。 

hello`QueueTrigger`屬性繫結 hello `inputText` hello 佇列訊息的參數 toohello 值。 和 hello`Blob`屬性繫結`TextWriter`物件 tooa blob 名為"blobname"中名為 「 容器名稱 」 的容器。  

        public static void ProcessQueueMessage([QueueTrigger("webjobsqueue")]] string inputText, 
            [Blob("containername/blobname")]TextWriter writer)

hello 函式，然後使用 hello 佇列訊息 toohello blob 這些參數 toowrite hello 值：

        writer.WriteLine(inputText);

hello hello WebJobs SDK 的觸發程序和繫結器功能大幅簡化您有 toowrite hello 程式碼。 hello 低層級所需的程式碼 tooprocess 佇列、 blob 或檔案或 tooinitiate 排定工作，會為您完成以上 hello WebJobs SDK 架構。 例如，hello 架構建立並不存在的佇列、 開啟 hello 佇列、 讀取佇列訊息、 刪除佇列訊息，當處理完成時，會建立 blob 容器不存在於尚未，寫入 tooblobs，依此類推。

hello 下列程式碼範例顯示各種不同的觸發程序中一個 WebJob: `QueueTrigger`， `FileTrigger`， `WebHookTrigger`，和`ErrorTrigger`。 

```
    public class Functions
    {
        public static void ProcessQueueMessage([QueueTrigger("queue")] string message,
        TextWriter log)
        {
            log.WriteLine(message);
        }

        public static void ProcessFileAndUploadToBlob(
            [FileTrigger(@"import\{name}", "*.*", autoDelete: true)] Stream file,
            [Blob(@"processed/{name}", FileAccess.Write)] Stream output,
            string name,
            TextWriter log)
        {
            output = file;
            file.Close();
            log.WriteLine(string.Format("Processed input file '{0}'!", name));
        }

        [Singleton]
        public static void ProcessWebHookA([WebHookTrigger] string body, TextWriter log)
        {
            log.WriteLine(string.Format("WebHookA invoked! Body: {0}", body));
        }

        public static void ProcessGitHubWebHook([WebHookTrigger] string body, TextWriter log)
        {
            dynamic issueEvent = JObject.Parse(body);
            log.WriteLine(string.Format("GitHub WebHook invoked! ('{0}', '{1}')",
                issueEvent.issue.title, issueEvent.action));
        }

        public static void ErrorMonitor(
        [ErrorTrigger("00:01:00", 1)] TraceFilter filter, TextWriter log,
        [SendGrid(
            too= "admin@emailaddress.com",
            Subject = "Error!")]
         SendGridMessage message)
        {
            // log last 5 detailed errors toohello Dashboard
            log.WriteLine(filter.GetDetailedMessage(5));
            message.Text = filter.GetDetailedMessage(1);
        }
    }
```

## <a id="schedule"></a> 排程
hello`TimerTrigger`屬性可提供 hello 能力 tootrigger 函式 toorun 的排程。 因為整個透過 Azure 或排程個別函式的 WebJob 使用 hello WebJobs SDK，您可以排程 WebJob `TimerTrigger`。 以下是程式碼範例。

```
public class Functions
{
    public static void ProcessTimer([TimerTrigger("*/15 * * * * *", RunOnStartup = true)]
    TimerInfo info, [Queue("queue")] out string message)
    {
        message = info.FormatNextOccurrences(1);
    }
}
```

如需範例程式碼，請參閱[TimerSamples.cs](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/ExtensionsSample/Samples/TimerSamples.cs)上 GitHub.com hello azure webjobs sdk-副檔名儲存機制中。

## <a name="extensibility"></a>擴充性
Toobuilt 中不受限於功能-hello WebJobs SDK 可讓您 toowrite 自訂觸發程序和繫結器。  例如，您可以撰寫用於快取事件和定期排程的觸發程序。 [開放原始碼儲存機制](https://github.com/Azure/azure-webjobs-sdk-extensions)包含[上 WebJobs SDK 擴充性的詳細的指引](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview)和範例程式碼 toohelp 協助您開始撰寫您自己的觸發程序和繫結器。

## <a id="workerrole"></a>使用 hello 之外 WebJobs WebJobs SDK
使用 WebJobs SDK 是標準的主控台應用程式，且可以執行任何位置-hello hello 的程式不一定 toorun webjob。 在開發電腦，並在生產環境，您可以執行中雲端服務背景工作角色或 Windows 服務如果您偏好其中一個這些環境中，您可以在本機測試 hello 程式。 

不過，hello 儀表板才會為 Azure App Service web 應用程式的延伸模組。 如果您想 toorun WebJob 之外，且仍使用 hello 儀表板，您可以設定 web 應用程式 toouse hello 相同儲存體帳戶是指您 WebJobs SDK 儀表板的連接字串，以及該 web 應用程式的 WebJobs 儀表板會顯示有關函數的資料從您的程式執行的其他地方執行。 您可以取得 toohello 儀表板使用 hello URL https://*{webappname}*.scm.azurewebsites.net/azurejobs/#/functions。 如需詳細資訊，請參閱[儀表板取得以 hello WebJobs SDK 的本機開發](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx)，但請注意 hello 部落格文章，顯示舊的連接字串名稱。 

## <a id="nostorage"></a>儀表板功能
即使您不使用 WebJobs SDK 觸發程序或繫結器 hello WebJobs SDK 會提供數個優點：

* 您可以叫用函式從 hello 儀表板。
* 您可以重新執行函式從 hello 儀表板。
* 您可以檢視記錄檔中 hello 儀表板連結 toohello 特定 WebJob （應用程式記錄檔，寫入使用 Console.Out、 Console.Error、 追蹤等） 或連結 toohello 特定函式引動過程產生它們 (使用所撰寫的記錄檔`TextWriter`物件的 hello SDK 將 toohello 函式做為參數）。 

如需詳細資訊，請參閱[toomanually 如何叫用函式](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual)和[toowrite 的記錄檔](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs) 

## <a id="nextsteps"></a>接續步驟
如需 hello WebJobs SDK 的詳細資訊，請參閱[Azure WebJobs 建議資源](http://go.microsoft.com/fwlink/?linkid=390226)。

如需最新增強功能 toohello hello WebJobs SDK 資訊，請參閱 hello[版本資訊](https://github.com/Azure/azure-webjobs-sdk/wiki/Release-Notes)。

