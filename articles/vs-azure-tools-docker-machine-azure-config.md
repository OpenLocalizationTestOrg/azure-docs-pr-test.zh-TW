---
title: "aaaCreate Docker 裝載於 Azure 的 Docker 機器 |Microsoft 文件"
description: "說明使用 Docker 機器 toocreate docker 主機，在 Azure 中。"
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 7a3ff6e1-fa93-4a62-b524-ab182d2fea08
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: fbf67e8189bbf33f874c4a9b619a931f28ccee12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-docker-hosts-in-azure-with-docker-machine"></a>使用 Docker-Machine 在 Azure 中建立 Docker 主機
執行[Docker](https://www.docker.com/)容器需要主機 VM 執行 hello docker 精靈。
本主題描述如何 toouse hello [docker 機器](https://docs.docker.com/machine/)toocreate 新 Linux Vm，以設定 hello Docker 精靈，在 Azure 中執行的命令。 

**附註：** 

* *本文是依據 docker-machine 0.9.0-rc2 版或更新版本*
* *Windows 容器將會支援透過 docker-機器在未來附近 hello*

## <a name="create-vms-with-docker-machine"></a>使用 Docker 電腦建立 VM
Docker 主機 Vm 在 Azure 中建立以 hello`docker-machine create`命令使用 hello`azure`驅動程式。 

hello Azure 驅動程式需要您的訂用帳戶 id。 您可以使用 hello [Azure CLI](cli-install-nodejs.md)或 hello [Azure 入口網站](https://portal.azure.com)tooretrieve 您 Azure 訂用帳戶。 

**使用 hello Azure 入口網站**

* 選取**訂閱**hello 左側瀏覽頁面以及複製 hello 訂用帳戶識別碼。

**使用 Azure CLI hello**

* 型別```azure account list```和複製 hello 訂用帳戶 id。

型別`docker-machine create --driver azure`toosee hello 選項和其預設值。
您也可以查看 hello [Docker Azure 驅動程式文件](https://docs.docker.com/machine/drivers/azure/)如需詳細資訊。 

hello 下列範例會依賴 hello[預設值](https://github.com/docker/machine/blob/master/drivers/azure/azure.go#L22)，但選擇性地設定這些值： 

* azure dns hello hello 公用 IP 相關聯的名稱，以及產生的憑證。 這是您的虛擬機器的 hello DNS 名稱。 hello VM 可以然後安全地停止，釋放 hello 動態 IP，並提供 hello 能力 tooreconnect 之後 hello vm 重新啟動新的 ip。 hello 名稱前置詞必須是唯一的 UNIQUE_DNSNAME_PREFIX.westus.cloudapp.azure.com 該區域。
* 開啟通訊埠 80 上 hello VM 為傳出網際網路存取
* hello VM tooutilize 快高階儲存體的大小
* 用於 hello vm 磁碟的進階儲存體

```
docker-machine create -d azure --azure-subscription-id <Your AZURE_SUBSCRIPTION_ID> --azure-dns <Your UNIQUE_DNSNAME_PREFIX> --azure-open-port 80 --azure-size Standard_DS1_v2 --azure-storage-type "Premium_LRS" mydockerhost 
```

## <a name="choose-a-docker-host-with-docker-machine"></a>使用 docker-machine 選擇 Docker 主機
一旦您擁有 docker 機器中的項目為您的主機，您可以設定 hello 預設主控件執行 docker 命令時。

## <a name="using-powershell"></a>使用 PowerShell
```powershell
docker-machine env MyDockerHost | Invoke-Expression 
```

## <a name="using-bash"></a>使用 Bash
```bash
eval $(docker-machine env MyDockerHost)
```

您現在可以針對 hello 指定的主機執行 docker 命令

```
docker ps
docker info
```

## <a name="run-a-container"></a>執行容器
請使用設定的主機，您現在可以執行簡單的 web 伺服器 tootest 是否已正確設定您的主機。
這裡我們使用的標準 nginx 映像，請指定應接聽連接埠 80，與 hello 主機 VM 重新啟動時，如果 hello 容器會重新啟動也 (`--restart=always`)。 

```bash
docker run -d -p 80:80 --restart=always nginx
```

hello 輸出看起來應該類似下列 hello:

```
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
83f52fbfa5f8: Pull complete
fa664caa1402: Pull complete
Digest: sha256:12127e07a75bda1022fbd4ea231f5527a1899aad4679e3940482db3b57383b1d
Status: Downloaded newer image for nginx:latest
25942c35d86fe43c688d0c03ad478f14cc9c16913b0e1c2971cb32eb4d0ab721
```

## <a name="test-hello-container"></a>測試 hello 容器
使用 `docker ps`檢查執行中容器：

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                         NAMES
d5b78f27b335        nginx               "nginx -g 'daemon off"   5 minutes ago       Up 5 minutes        0.0.0.0:80->80/tcp, 443/tcp   goofy_mahavira
```

和執行類型的容器，toosee hello `docker-machine ip <VM name>` toofind hello IP 位址 tooenter hello 瀏覽器中：

```
PS C:\> docker-machine ip MyDockerHost
191.237.46.90
```

![執行 ngnix 容器](./media/vs-azure-tools-docker-machine-azure-config/nginxsuccess.png)

## <a name="summary"></a>摘要
docker-machine 可讓您在 Azure 中輕鬆地佈建 docker 主機，以進行個別 docker 主機驗證。
生產環境裝載的容器，請參閱 hello [Azure 容器服務](http://aka.ms/AzureContainerService)

toodevelop.NET Core 應用程式與 Visual Studio，請參閱[Docker Tools for Visual Studio](http://aka.ms/DockerToolsForVS)

