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
# <a name="configure-a-docker-host-with-virtualbox"></a>使用 VirtualBox 設定 Docker 主機
## <a name="overview"></a>Overview
本文會逐步引導您使用 Docker 機器和 VirtualBox 來設定預設 Docker 執行個體。 如果您使用 hello [Docker for Windows beta](http://beta.docker.com/)，不需要此設定。

## <a name="prerequisites"></a>必要條件
hello 下列工具需要 toobe 安裝。

* [Docker 工具箱](https://www.docker.com/products/overview#/docker_toolbox)

## <a name="configuring-hello-docker-client-with-windows-powershell"></a>使用 Windows PowerShell 設定 hello Docker 用戶端
tooconfigure Docker 用戶端，只要開啟 Windows PowerShell 並執行下列步驟的 hello:

1. 建立預設 Docker 主機執行個體。
   
    ```PowerShell
    docker-machine create --driver virtualbox default
    ```
2. 請確認 hello 預設執行個體已設定且正在執行。 (您應該會看到名為「default」的執行個體正在執行。
   
    ```PowerShell
    docker-machine ls 
    ```
   
    ![docker-machine ls 輸出][0]
3. 設為預設值為 hello 目前的主機，並設定您的 shell。
   
    ```PowerShell
    docker-machine env default | Invoke-Expression
    ```
4. 顯示 hello active Docker 容器。 hello 清單應該是空的。
   
    ```PowerShell
    docker ps
    ```
   
    ![docker ps 輸出][1]

> [!NOTE]
> 每次您重新啟動您的開發電腦，您將需要 toorestart 本機 docker 主機。
> toodo 下列命令，在命令提示字元中，問題 hello: `docker-machine start default`。
> 
> 

[0]: ./media/vs-azure-tools-docker-setup/docker-machine-ls.png
[1]: ./media/vs-azure-tools-docker-setup/docker-ps.png
