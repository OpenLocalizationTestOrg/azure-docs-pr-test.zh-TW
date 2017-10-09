---
title: "aaaUsing 適用於 Linux 的 Docker VM 擴充功能 |Microsoft 文件"
description: "描述 Docker 和 hello Azure 虛擬機器擴充功能，以及 toocreate docker 主機使用的 Azure 虛擬機器 hello Azure CLI 傳統部署模型中的方式。"
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 19cf64e8-f92c-43ad-a120-8976cd9102ac
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/27/2016
ms.author: rasquill
ms.openlocfilehash: 9d455b63c48b0c1b6f14862e072f899a73b46153
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-docker-vm-extension-with-hello-azure-classic-portal"></a>使用 hello Azure 傳統入口網站中的 hello Docker VM 擴充功能
> [!IMPORTANT] 
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。 本文件涵蓋使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。

[Docker](https://www.docker.com/)是 hello 的其中一個最普遍使用的虛擬化方法[Linux 容器](http://en.wikipedia.org/wiki/LXC)而不是虛擬機器做為隔離資料，並在共用資源上運算的方式。 您可以使用由管理的 hello Docker VM 擴充功能[Azure Linux 代理程式]toocreate 裝載任何數目的容器應用程式在 Azure 上的 Docker VM。

> [!NOTE]
> 本主題描述如何從 Docker VM 的 toocreate hello Azure 傳統入口網站。 如何 toocreate Docker VM 在 hello 命令列，請參閱的 toosee [toouse hello Azure 命令列介面 (Azure CLI) 從 hello Docker VM 擴充功能的方式]。 toosee 高層級容器和 lamdba 的優點的討論，請參閱 「 hello [Docker 高的層級抄寫](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard)。
> 
> 

## <a name="create-a-new-vm-from-hello-image-gallery"></a>從 hello 映像庫中建立新的 VM
hello 第一個步驟之前，必須從 Linux 映像支援 Docker VM 擴充功能，使用做為範例伺服器映像和 Ubuntu 14.04 桌面的 Ubuntu 14.04 LTS 從 hello 映像庫映像，做為用戶端 hello Azure VM。 在 hello 入口網站中，按一下  **+ 新增**在 hello 底部往左角 toocreate 新的 VM 執行個體，並選取從可用的 hello 選項或 hello Ubuntu 14.04 LTS 映像完成映像庫，如下所示。

> [!NOTE]
> 目前，只有 Ubuntu 14.04 LTS 映像以上 2014 年 7 月支援 hello Docker VM 擴充功能。
> 
> 

![Create a new Ubuntu Image](./media/portal-use-docker/ChooseUbuntu.png)

## <a name="create-docker-certificates"></a>建立 Docker 憑證
Hello 之後建立 VM，確定已安裝 Docker 用戶端電腦上。 (如需詳細資訊，請參閱 [Docker 安裝指示](https://docs.docker.com/installation/#installation)。)

建立 hello 太根據 Docker 通訊的憑證與金鑰檔案[執行 Docker https]並將它們放在 hello  **`~/.docker`** 目錄用戶端電腦上。

> [!NOTE]
> hello 入口網站中的 hello Docker VM 擴充功能目前需要是以 base64 編碼的認證。
> 
> 

在 hello 命令列使用 **`base64`** 或另一個編碼 tool toocreate base64 編碼主題的最愛。 執行此動作有一組簡單的憑證與金鑰檔案，可能看起來類似 toothis:

```
 ~/.docker$ ls
 ca-key.pem  ca.pem  cert.pem  key.pem  server-cert.pem  server-key.pem
 ~/.docker$ base64 ca.pem > ca64.pem
 ~/.docker$ base64 server-cert.pem > server-cert64.pem
 ~/.docker$ base64 server-key.pem > server-key64.pem
 ~/.docker$ ls
 ca64.pem    ca.pem    key.pem            server-cert.pem   server-key.pem
 ca-key.pem  cert.pem  server-cert64.pem  server-key64.pem
```

## <a name="add-hello-docker-vm-extension"></a>新增 hello Docker VM 擴充功能
tooadd hello Docker VM 擴充功能，找出您所建立的 hello VM 執行個體，並向下捲動太**延伸**按一下 toobring VM 延伸模組，如下所示。

> [!NOTE]
> Hello 預覽入口網站中支援這項功能： https://portal.azure.com/
> 
> 

![](media/portal-use-docker/ClickExtensions.png)

### <a name="add-an-extension"></a>新增擴充程式
按一下 hello **+ 加**toodisplay hello 可能可以新增 toothis VM 的 VM 擴充功能。

![](media/portal-use-docker/ClickAdd.png)

### <a name="select-hello-docker-vm-extension"></a>選取 hello Docker VM 擴充功能
選擇 hello Docker VM 擴充功能，這會顯示 hello Docker 描述和重要的連結，然後再按一下**建立**在 hello 底部 toobegin hello 安裝程序。

![](media/portal-use-docker/ChooseDockerExtension.png)

![](media/portal-use-docker/CreateButtonFocus.png)

### <a name="add-your-certificate-and-key-files"></a>新增憑證和金鑰檔案：
Hello 表單在欄位中，輸入 hello base64 編碼的版本您的 CA 憑證，您的伺服器憑證，而您的伺服器金鑰，hello 下列圖片所示。

![](media/portal-use-docker/AddExtensionFormFilled.png)

> [!NOTE]
> 請注意，（如同在上述映像的 hello) hello 2376 預設會填入。 您可以輸入任何端點，但是 hello 下一個步驟將會比對端點的 hello 向上 tooopen。 如果您變更 hello 預設值，請確定 tooopen 向上 hello 比對 hello 下一個步驟中的端點。
> 
> 

## <a name="add-hello-docker-communication-endpoint"></a>新增 hello Docker 通訊端點
當您檢視您已建立 hello 資源群組，選取與您的 VM 的網路安全性群組相關聯的 hello，然後按一下**輸入安全性規則**tooview hello 規則如下所示。

![](media/portal-use-docker/AddingEndpoint.png)

按一下**+ 加**tooadd 另一個規則，並在 hello 預設情況下，輸入 hello 端點的名稱 (在此範例中， **Docker**)，和 2376年 ' 目的地連接埠範圍 '。 設定 hello 通訊協定值顯示**TCP**，然後按一下**確定**toocreate hello 規則。

![](media/portal-use-docker/AddEndpointFormFilledOut.png)

## <a name="test-your-docker-client-and-azure-docker-host"></a>測試 Docker 用戶端和 Azure Docker 主機
找出並複製 VM 的網域，而且在 hello 命令列的用戶端電腦，類型的 hello 名稱`docker --tls -H tcp://` *dockerextension* `.cloudapp.net:2376 info` (其中*dockerextension*取代為 hello子網域的 VM）。

hello 結果應該會出現類似 toothis:

```
$ docker --tls -H tcp://dockerextension.cloudapp.net:2376 info
Containers: 0
Images: 0
Storage Driver: devicemapper
 Pool Name: docker-8:1-131214-pool
 Pool Blocksize: 65.54 kB
 Data file: /var/lib/docker/devicemapper/devicemapper/data
 Metadata file: /var/lib/docker/devicemapper/devicemapper/metadata
 Data Space Used: 305.7 MB
 Data Space Total: 107.4 GB
 Metadata Space Used: 729.1 kB
 Metadata Space Total: 2.147 GB
 Library Version: 1.02.82-git (2013-10-04)
Execution Driver: native-0.2
Kernel Version: 3.13.0-36-generic
WARNING: No swap limit support
```

一旦您完成上述步驟 hello，現在有完全正常運作的 Docker 主機，在 Azure VM 中，設定執行 toobe 連接 tooremotely 從其他用戶端。

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>後續步驟
您已準備好 toogo toohello [Docker 使用者指南]並使用您的 Docker VM。 如果您想 tooautomate 建立 Azure Vm 上的 Docker 主機，透過命令列介面時，請參閱[toouse hello Azure 命令列介面 (Azure CLI) 從 hello Docker VM 擴充功能的方式]

<!--Anchors-->
[Create a new VM from hello Image Gallery]:#createvm
[Create Docker Certificates]:#dockercerts
[Add hello Docker VM Extension]:#adddockerextension
[Test Docker Client and Azure Docker Host]:#testclientandserver
[Next steps]:#next-steps

<!--Image references-->
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[6]:./media/markdown-template-for-new-articles/pretty49.png
[7]:./media/markdown-template-for-new-articles/channel-9.png


<!--Link references-->
[toouse hello Azure 命令列介面 (Azure CLI) 從 hello Docker VM 擴充功能的方式]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-xplat-cli/
[Azure Linux 代理程式]:../agent-user-guide.md
[Link 3 tooanother azure.microsoft.com documentation topic]:../storage-whatis-account.md

[執行 Docker https]:http://docs.docker.com/articles/https/
[Docker 使用者指南]:https://docs.docker.com/userguide/
