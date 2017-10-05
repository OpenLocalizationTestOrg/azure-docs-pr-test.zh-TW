---
title: "在 Linux 上的 Azure Web 應用程式中使用適用於 Node.js 的 PM2 組態 | Microsoft Docs"
description: "在 Linux 上的 Azure Web 應用程式中使用適用於 Node.js 的 PM2 組態"
keywords: "azure app service, web 應用程式, nodejs, pm2, linux, oss"
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: fb420f32-6d74-49c7-992f-0ed5616e66e7
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 5002400a673e2c5cc4290bab488b839fb2282966
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="use-pm2-configuration-for-nodejs-in-azure-web-app-on-linux"></a><span data-ttu-id="a4e4c-104">在 Linux 上的 Azure Web 應用程式中使用適用於 Node.js 的 PM2 組態</span><span class="sxs-lookup"><span data-stu-id="a4e4c-104">Use PM2 configuration for Node.js in Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


<span data-ttu-id="a4e4c-105">針對 Linux 上的 Azure Web 應用程式，如果您將應用程式堆疊設定為 Node.js，就可以選擇設定 Node.js 啟動檔案，如下列映像所示：</span><span class="sxs-lookup"><span data-stu-id="a4e4c-105">If you set the application stack to Node.js for Azure Web App on Linux, you get the option to set a Node.js startup file as shown in the following image:</span></span>

![設定 Node.js 啟動檔案][1]

<span data-ttu-id="a4e4c-107">您可以使用此選項來執行下列工作︰</span><span class="sxs-lookup"><span data-stu-id="a4e4c-107">You can use this option to do one of the following tasks:</span></span>

* <span data-ttu-id="a4e4c-108">指定 Node.js 應用程式的啟動指令碼 (例如︰/bin/server.js)。</span><span class="sxs-lookup"><span data-stu-id="a4e4c-108">Specify the startup script for your Node.js app (for example: /bin/server.js).</span></span>
* <span data-ttu-id="a4e4c-109">指定要用於 Node.js 應用程式的 PM2 組態檔 (例如︰/foo/process.json)。</span><span class="sxs-lookup"><span data-stu-id="a4e4c-109">Specify the PM2 configuration file to use for your Node.js app (for example: /foo/process.json).</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="a4e4c-110">如果您想要在修改某些檔案時自動重新啟動您的 Node.js 程序，請使用 PM2 組態。</span><span class="sxs-lookup"><span data-stu-id="a4e4c-110">If you want your Node.js processes to restart automatically when certain files are modified, use the PM2 configuration.</span></span> <span data-ttu-id="a4e4c-111">否則，應用程式收到變更通知時不會重新啟動 (例如，當應用程式的程式碼變更時)。</span><span class="sxs-lookup"><span data-stu-id="a4e4c-111">Otherwise, your application won't restart when it receives change notifications (for example, when your application code changes).</span></span>
  > 
  > 

<span data-ttu-id="a4e4c-112">您可以在 Node.js [處理檔案文件](http://pm2.keymetrics.io/docs/usage/application-declaration/)中查看所有選項，以下只是可作為 process.json 檔案的範例︰</span><span class="sxs-lookup"><span data-stu-id="a4e4c-112">You can check the Node.js [process file documentation](http://pm2.keymetrics.io/docs/usage/application-declaration/) for all the options, but following is a sample of what you can use as your process.json file:</span></span>

        {
          "name"        : "worker",
          "script"      : "./bin/server.js",
          "instances"   : 1,
          "merge_logs"  : true,
          "log_date_format" : "YYYY-MM-DD HH:mm Z",
          "watch": ["./bin/server.js", "foo.txt"],
          "watch_options": {
            "followSymlinks": true,
            "usePolling"   : true,
            "interval"    : 5
          }
        }

<span data-ttu-id="a4e4c-113">此組態中的重要注意事項如下︰</span><span class="sxs-lookup"><span data-stu-id="a4e4c-113">Important things to note in this configuration are:</span></span>

* <span data-ttu-id="a4e4c-114">"script" 屬性指定應用程式的啟動指令碼。</span><span class="sxs-lookup"><span data-stu-id="a4e4c-114">The "script" property specifies your application's start script.</span></span>
* <span data-ttu-id="a4e4c-115">"instances" 屬性指定節點程序要啟動的執行個體數目。</span><span class="sxs-lookup"><span data-stu-id="a4e4c-115">The "instances" property specifies how many instances of the node process to launch.</span></span> <span data-ttu-id="a4e4c-116">如果您在有多個核心的較大 VM 上執行應用程式，最好設定較高的值，以充分運用資源。</span><span class="sxs-lookup"><span data-stu-id="a4e4c-116">If you are running your application on larger VMs that have multiple cores, it's a good idea to maximize your resources by setting a higher value here.</span></span>
* <span data-ttu-id="a4e4c-117">"watch" 陣列指定造成您想要重新啟動節點程序的所有檔案 (當它們變更時)。</span><span class="sxs-lookup"><span data-stu-id="a4e4c-117">The "watch" array specifies all files that you want to restart the node process for when they change.</span></span>
* <span data-ttu-id="a4e4c-118">針對 "watch_options"，由於應用程式內容的裝載方式，您目前需要將 "usePolling" 指定為 true。</span><span class="sxs-lookup"><span data-stu-id="a4e4c-118">For the "watch_options", you currently need to specify "usePolling" as true because of the way your application content is mounted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a4e4c-119">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a4e4c-119">Next steps</span></span>
* [<span data-ttu-id="a4e4c-120">什麼是 Linux 上的 Azure Web 應用程式？</span><span class="sxs-lookup"><span data-stu-id="a4e4c-120">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="a4e4c-121">Linux 上的 Azure App Service Web 應用程式常見問題集</span><span class="sxs-lookup"><span data-stu-id="a4e4c-121">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-nodejs-pm2/nodejs-startup-file.png
