---
title: "aaaApplication 或特定使用者馬拉松服務 |Microsoft 文件"
description: "建立應用程式或使用者特定的 Marathon 服務"
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "容器, Marathon, 微服務, DC/OS, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/12/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 1e6f69ed64e113a3a059788a71ddb57b6d3ad8da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-or-user-specific-marathon-service"></a><span data-ttu-id="dc33c-104">建立應用程式或使用者特定的 Marathon 服務</span><span class="sxs-lookup"><span data-stu-id="dc33c-104">Create an application or user-specific Marathon service</span></span>
<span data-ttu-id="dc33c-105">Azure Container Service 提供了一組主要伺服器，供我們在上面預先設定 Apache Mesos 和 Marathon。</span><span class="sxs-lookup"><span data-stu-id="dc33c-105">Azure Container Service provides a set of master servers on which we preconfigure Apache Mesos and Marathon.</span></span> <span data-ttu-id="dc33c-106">這些可以是使用的 tooorchestrate 上 hello 叢集中，但該應用程式針對此用途的最佳不 toouse hello 主要伺服器。</span><span class="sxs-lookup"><span data-stu-id="dc33c-106">These can be used tooorchestrate your applications on hello cluster, but it's best not toouse hello master servers for this purpose.</span></span> <span data-ttu-id="dc33c-107">例如，調整馬拉松 hello 組態需要登入 hello 主要伺服器本身，並進行變更-這鼓勵唯一的方式稍有不同於標準的 hello 和需要 toobe 在意這次的及受管理的主要伺服器獨立。</span><span class="sxs-lookup"><span data-stu-id="dc33c-107">For example, tweaking hello configuration of Marathon requires logging into hello master servers themselves and making changes--this encourages unique master servers that are a little different from hello standard and need toobe cared for and managed independently.</span></span> <span data-ttu-id="dc33c-108">此外，一個小組所需要的 hello 組態可能不是 hello 為其他小組的最佳組態。</span><span class="sxs-lookup"><span data-stu-id="dc33c-108">Additionally, hello configuration required by one team might not be hello optimal configuration for another team.</span></span>

<span data-ttu-id="dc33c-109">在本文中，我們將說明如何 tooadd 應用程式或使用者特定馬拉松服務。</span><span class="sxs-lookup"><span data-stu-id="dc33c-109">In this article, we'll explain how tooadd an application or user-specific Marathon service.</span></span>

<span data-ttu-id="dc33c-110">是免費 tooconfigure tooa 單一使用者或小組，將屬於這個服務，因為它以任何他們想要的方式。</span><span class="sxs-lookup"><span data-stu-id="dc33c-110">Because this service will belong tooa single user or team, they are free tooconfigure it in any way that they desire.</span></span> <span data-ttu-id="dc33c-111">此外，Azure 容器服務可確保 hello 服務仍維持 toorun。</span><span class="sxs-lookup"><span data-stu-id="dc33c-111">Also, Azure Container Service will ensure that hello service continues toorun.</span></span> <span data-ttu-id="dc33c-112">如果 hello 服務失敗時，Azure 容器服務將會重新啟動它為您。</span><span class="sxs-lookup"><span data-stu-id="dc33c-112">If hello service fails, Azure Container Service will restart it for you.</span></span> <span data-ttu-id="dc33c-113">大部分的 hello 時間您將不會注意它有停機時間。</span><span class="sxs-lookup"><span data-stu-id="dc33c-113">Most of hello time you won't even notice it had downtime.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dc33c-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="dc33c-114">Prerequisites</span></span>
<span data-ttu-id="dc33c-115">[部署 Azure 容器服務的執行個體](container-service-deployment.md)與 orchestrator 輸入 DC/OS 和[確定您的用戶端可以連線 tooyour 叢集](../container-service-connect.md)。</span><span class="sxs-lookup"><span data-stu-id="dc33c-115">[Deploy an instance of Azure Container Service](container-service-deployment.md) with orchestrator type DC/OS and  [ensure that your client can connect tooyour cluster](../container-service-connect.md).</span></span> <span data-ttu-id="dc33c-116">此外，請勿 hello 下列步驟。</span><span class="sxs-lookup"><span data-stu-id="dc33c-116">Also, do hello following steps.</span></span>

[!INCLUDE [install hello DC/OS CLI](../../../includes/container-service-install-dcos-cli-include.md)]

## <a name="create-an-application-or-user-specific-marathon-service"></a><span data-ttu-id="dc33c-117">建立應用程式或使用者特定的 Marathon 服務</span><span class="sxs-lookup"><span data-stu-id="dc33c-117">Create an application or user-specific Marathon service</span></span>
<span data-ttu-id="dc33c-118">開始建立定義 hello 名稱的 toocreate hello 應用程式服務的 JSON 組態檔。</span><span class="sxs-lookup"><span data-stu-id="dc33c-118">Begin by creating a JSON configuration file that defines hello name of hello application service that you want toocreate.</span></span> <span data-ttu-id="dc33c-119">我們在此使用`marathon-alice`為 hello 架構名稱。</span><span class="sxs-lookup"><span data-stu-id="dc33c-119">Here we use `marathon-alice` as hello framework name.</span></span> <span data-ttu-id="dc33c-120">將 hello 檔案儲存為類似`marathon-alice.json`:</span><span class="sxs-lookup"><span data-stu-id="dc33c-120">Save hello file as something like `marathon-alice.json`:</span></span>

```json
{"marathon": {"framework-name": "marathon-alice" }}
```

<span data-ttu-id="dc33c-121">接下來，使用組態檔中所設定的 hello 選項 hello DC/OS CLI tooinstall hello 馬拉松執行個體：</span><span class="sxs-lookup"><span data-stu-id="dc33c-121">Next, use hello DC/OS CLI tooinstall hello Marathon instance with hello options that are set in your configuration file:</span></span>

```bash
dcos package install --options=marathon-alice.json marathon
```

<span data-ttu-id="dc33c-122">您現在應該會看到您`marathon-alice`hello DC/OS UI 的 [服務] 索引標籤中執行的服務。</span><span class="sxs-lookup"><span data-stu-id="dc33c-122">You should now see your `marathon-alice` service running in hello Services tab of your DC/OS UI.</span></span> <span data-ttu-id="dc33c-123">hello 會在 UI`http://<hostname>/service/marathon-alice/`如果您想 tooaccess 它直接。</span><span class="sxs-lookup"><span data-stu-id="dc33c-123">hello UI will be `http://<hostname>/service/marathon-alice/` if you want tooaccess it directly.</span></span>

## <a name="set-hello-dcos-cli-tooaccess-hello-service"></a><span data-ttu-id="dc33c-124">設定 hello DC/OS CLI tooaccess hello 服務</span><span class="sxs-lookup"><span data-stu-id="dc33c-124">Set hello DC/OS CLI tooaccess hello service</span></span>
<span data-ttu-id="dc33c-125">您可以選擇性地設定 DC/OS CLI tooaccess 這個新服務所設定的 hello`marathon.url`屬性 toopoint toohello`marathon-alice`執行個體，如下所示：</span><span class="sxs-lookup"><span data-stu-id="dc33c-125">You can optionally configure your DC/OS CLI tooaccess this new service by setting hello `marathon.url` property toopoint toohello `marathon-alice` instance as follows:</span></span>

```bash
dcos config set marathon.url http://<hostname>/service/marathon-alice/
```

<span data-ttu-id="dc33c-126">您可以確認哪一個執行個體的 CLI 您正在針對與 hello 的馬拉松`dcos config show`命令。</span><span class="sxs-lookup"><span data-stu-id="dc33c-126">You can verify which instance of Marathon that your CLI is working against with hello `dcos config show` command.</span></span> <span data-ttu-id="dc33c-127">您可以還原 toousing hello 命令與您主要馬拉松服務`dcos config unset marathon.url`。</span><span class="sxs-lookup"><span data-stu-id="dc33c-127">You can revert toousing your master Marathon service with hello command `dcos config unset marathon.url`.</span></span>

