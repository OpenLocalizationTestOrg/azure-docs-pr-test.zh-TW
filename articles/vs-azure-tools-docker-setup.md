---
title: "aaaConfigure VirtualBox Docker 主機 |Microsoft 文件"
description: "使用 Docker 機器和 VirtualBox Docker 預設執行個體的逐步指示 tooconfigure"
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 0b1335a2-7720-42a8-8260-4e06fc00c9f6
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: 1df2da4482444a803d05e413e019edcc57269062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-docker-host-with-virtualbox"></a><span data-ttu-id="0f719-103">使用 VirtualBox 設定 Docker 主機</span><span class="sxs-lookup"><span data-stu-id="0f719-103">Configure a Docker Host with VirtualBox</span></span>
## <a name="overview"></a><span data-ttu-id="0f719-104">Overview</span><span class="sxs-lookup"><span data-stu-id="0f719-104">Overview</span></span>
<span data-ttu-id="0f719-105">本文會逐步引導您使用 Docker 機器和 VirtualBox 來設定預設 Docker 執行個體。</span><span class="sxs-lookup"><span data-stu-id="0f719-105">This article guides you through configuring a default Docker instance using Docker Machine and VirtualBox.</span></span> <span data-ttu-id="0f719-106">如果您使用 hello [Docker for Windows beta](http://beta.docker.com/)，不需要此設定。</span><span class="sxs-lookup"><span data-stu-id="0f719-106">If you’re using hello [Docker for Windows beta](http://beta.docker.com/), this configuration is not necessary.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0f719-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="0f719-107">Prerequisites</span></span>
<span data-ttu-id="0f719-108">hello 下列工具需要 toobe 安裝。</span><span class="sxs-lookup"><span data-stu-id="0f719-108">hello following tools need toobe installed.</span></span>

* [<span data-ttu-id="0f719-109">Docker 工具箱</span><span class="sxs-lookup"><span data-stu-id="0f719-109">Docker Toolbox</span></span>](https://www.docker.com/products/overview#/docker_toolbox)

## <a name="configuring-hello-docker-client-with-windows-powershell"></a><span data-ttu-id="0f719-110">使用 Windows PowerShell 設定 hello Docker 用戶端</span><span class="sxs-lookup"><span data-stu-id="0f719-110">Configuring hello Docker client with Windows PowerShell</span></span>
<span data-ttu-id="0f719-111">tooconfigure Docker 用戶端，只要開啟 Windows PowerShell 並執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="0f719-111">tooconfigure a Docker client, simply open Windows PowerShell, and perform hello following steps:</span></span>

1. <span data-ttu-id="0f719-112">建立預設 Docker 主機執行個體。</span><span class="sxs-lookup"><span data-stu-id="0f719-112">Create a default docker host instance.</span></span>
   
    ```PowerShell
    docker-machine create --driver virtualbox default
    ```
2. <span data-ttu-id="0f719-113">請確認 hello 預設執行個體已設定且正在執行。</span><span class="sxs-lookup"><span data-stu-id="0f719-113">Verify hello default instance is configured and running.</span></span> <span data-ttu-id="0f719-114">(您應該會看到名為「default」的執行個體正在執行。</span><span class="sxs-lookup"><span data-stu-id="0f719-114">(You should see an instance named \`default' running.</span></span>
   
    ```PowerShell
    docker-machine ls 
    ```
   
    ![docker-machine ls 輸出][0]
3. <span data-ttu-id="0f719-116">設為預設值為 hello 目前的主機，並設定您的 shell。</span><span class="sxs-lookup"><span data-stu-id="0f719-116">Set default as hello current host, and configure your shell.</span></span>
   
    ```PowerShell
    docker-machine env default | Invoke-Expression
    ```
4. <span data-ttu-id="0f719-117">顯示 hello active Docker 容器。</span><span class="sxs-lookup"><span data-stu-id="0f719-117">Display hello active Docker containers.</span></span> <span data-ttu-id="0f719-118">hello 清單應該是空的。</span><span class="sxs-lookup"><span data-stu-id="0f719-118">hello list should be empty.</span></span>
   
    ```PowerShell
    docker ps
    ```
   
    ![docker ps 輸出][1]

> [!NOTE]
> <span data-ttu-id="0f719-120">每次您重新啟動您的開發電腦，您將需要 toorestart 本機 docker 主機。</span><span class="sxs-lookup"><span data-stu-id="0f719-120">Each time you reboot your development machine, you’ll need toorestart your local docker host.</span></span>
> <span data-ttu-id="0f719-121">toodo 下列命令，在命令提示字元中，問題 hello: `docker-machine start default`。</span><span class="sxs-lookup"><span data-stu-id="0f719-121">toodo this, issue hello following command at a command prompt: `docker-machine start default`.</span></span>
> 
> 

[0]: ./media/vs-azure-tools-docker-setup/docker-machine-ls.png
[1]: ./media/vs-azure-tools-docker-setup/docker-ps.png
