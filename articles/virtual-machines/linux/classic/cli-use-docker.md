---
title: "aaaUsing hello Linux on Azure 的 Docker VM 延伸模組"
description: "描述 Docker 和 hello Azure 虛擬機器擴充功能，並示範 tooprogrammatically Azure 的 docker 主機使用 Azure CLI hello hello 命令列上所建立的虛擬機器。"
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: eaff75e3-d929-4931-a4a1-8c377a8e7302
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 08/29/2016
ms.author: rasquill
ms.openlocfilehash: 1e192ad7c273aa9c997ea7bfa53b7de0b41a43c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-docker-vm-extension-from-hello-azure-command-line-interface-azure-cli"></a>使用從 hello Azure 命令列介面 (Azure CLI) hello Docker VM 擴充功能
> [!IMPORTANT] 
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。 本文件涵蓋使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。 如需搭配 hello 資源管理員模型使用 hello Docker VM 擴充功能資訊，請參閱[這裡](../dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

本主題描述如何 toocreate 具有從 hello hello Docker VM 擴充功能的 VM 服務在 Azure CLI 任何平台上的管理 (asm) 模式。 [Docker](https://www.docker.com/)是 hello 的其中一個最普遍使用的虛擬化方法[Linux 容器](http://en.wikipedia.org/wiki/LXC)而不是虛擬機器做為隔離資料，並在共用資源上運算的方式。 您可以使用 hello Docker VM 擴充功能和 hello [Azure Linux 代理程式](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)toocreate 裝載任何數目的容器應用程式在 Azure 上的 Docker VM。 toosee 高層級容器和 lamdba 的優點的討論，請參閱 「 hello [Docker 高的層級抄寫](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard)。

## <a name="how-toouse-hello-docker-vm-extension-with-azure"></a>如何 toouse hello 與 Azure 的 Docker VM 擴充功能
toouse 與 Azure 的 hello Docker VM 擴充功能，您必須安裝新版 hello [Azure 命令列介面](https://github.com/Azure/azure-sdk-tools-xplat)(Azure CLI) 高於 0.8.6 （如這個寫入 hello 的目前版本是 0.10.0）。 您可以安裝 hello Azure CLI Mac、 Linux 及 Windows 上。

hello 完整程序 toouse Azure 上的 Docker 很簡單：

* 要從中 toocontrol Azure 的 hello 電腦上安裝 hello Azure CLI 和其相依性 （在 Windows 中，這將會執行為虛擬機器的 Linux 散發套件）
* 在 Azure 中使用 hello Azure CLI Docker 命令 toocreate VM Docker 主機
* 在您的 Docker VM 在 Azure 中使用本機 Docker 命令 toomanage hello Docker 容器。

### <a name="install-hello-azure-command-line-interface-azure-cli"></a>安裝 Azure 命令列介面 (Azure CLI) hello
tooinstall 和設定 hello Azure CLI，請參閱[tooinstall hello Azure 命令列介面的方式](../../../cli-install-nodejs.md)。 tooconfirm hello 安裝類型`azure`hello 的命令提示字元，並在短時間之後您應該會看見 hello Azure CLI ASCII 封面，列出 hello basic 命令可用 tooyou。 如果 hello 安裝正確運作，您應該能夠 tootype`azure help vm`看到其中一個列出的 hello 命令為"docker"。

> [!NOTE]
> Docker 有工具適用於 Windows、 [Docker 機器](https://docs.docker.com/installation/windows/)，而您也可以使用 docker 用戶端，您可以為 docker 主機與 Azure Vm 搭配使用 toowork tooautomate hello 建立。
> 
> 

### <a name="connect-hello-azure-cli-tootooyour-azure-account"></a>連接 hello Azure CLI tootooyour Azure 帳戶
您可以使用 Azure CLI hello 之前必須以 hello Azure CLI 平台上對您的 Azure 帳戶的認證進行關聯。 hello 區段[如何 tooconnect tooyour Azure 訂用帳戶](../../../xplat-cli-connect.md)說明 tooeither 如何下載和匯入您**.publishsettings**檔案，或將 Azure CLI 與組織識別碼產生關聯。

> [!NOTE]
> 有一些行為差異時使用其中一種或 hello 其他方法的驗證，因此務必確定上述 toounderstand hello 不同功能的 tooread hello 文件。
> 
> 

### <a name="install-docker-and-use-hello-docker-vm-extension-for-azure"></a>將 Docker 安裝和使用 Azure 的 hello Docker VM 擴充功能
請遵循 hello [Docker 安裝指示](https://docs.docker.com/installation/#installation)tooinstall Docker 在本機電腦上的。

toouse Docker 的 Azure 虛擬機器，用於 hello VM 的 hello Linux 映像必須已在 hello [Azure Linux VM 代理程式](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)安裝。 目前來說，只有兩種映像類型提供此安裝：

* Ubuntu 從 hello Azure 映像庫映像或
* 自訂的 Linux 映像，您已建立以 hello Azure Linux VM 代理程式安裝和設定。 請參閱[Azure Linux VM 代理程式](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)如需有關如何 toobuild 自訂 Linux VM 以 hello Azure VM 代理程式。

### <a name="using-hello-azure-image-gallery"></a>使用 hello Azure 映像庫
從 Bash 或終端機工作階段中，使用下列 Azure CLI 命令 toolocate 輸入 hello hello VM 圖庫 toouse 中的最新 Ubuntu 映像的 hello

`azure vm image list | grep Ubuntu-14_04`

選取其中一個 hello 映像名稱，例如`b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB`，並使用 hello 下列命令 toocreate 使用該映像的新 VM。

```
azure vm docker create -e 22 -l "West US" <vm-cloudservice name> "b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB" <username> <password>
```

其中：

* *&lt;vm cloudservice 名稱&gt;* hello hello 會變成 hello Docker 容器主機電腦在 Azure 中的 VM 名稱
* *&lt;使用者名稱&gt;* hello hello 預設根使用者的 hello VM 的使用者名稱
* *&lt;密碼&gt;* hello 密碼的 hello *username*帳戶符合 azure 的 hello 標準的複雜性

> [!NOTE]
> 目前的密碼必須至少為 8 個字元、 包含一個小寫和一個大寫字元、 數字和特殊字元，例如其中一個 hello 下列字元： `!@#$%^&+=`。 否，hello 期間在 hello hello 前面句子的結尾不是特殊字元。
> 
> 

如果 hello 命令執行成功，您應該會看到類似 hello 下列程式碼，根據 hello 精確引數和您所使用的選項：

![](media/cli-use-docker/dockercreateresults.png)

> [!NOTE]
> 建立虛擬機器可能需要幾分鐘的時間，但已佈建它之後 (hello 狀態值是`ReadyRole`) hello Docker daemon (hello Docker 服務) 啟動，而且您可以連線 toohello Docker 容器主機。
> 
> 

tootest hello Docker VM，您已建立在 Azure 中，類型

`docker --tls -H tcp://<vm-name-you-used>.cloudapp.net:2376 info`

其中 *&lt;vm--您為使用名稱&gt;* hello hello 過您的呼叫中使用的虛擬機器名稱`azure vm docker create`。 您應該會看到類似 toohello 下列程式碼，這表示您的 Docker 主機 VM 已啟動並在 Azure 中執行並等候命令。 

現在您可以嘗試使用您的 docker 用戶端 tooobtain 資訊 tooconnect (在某些 Docker 用戶端設定，例如，在 Mac 上，您可能會有 toouse `sudo`):

    sudo docker --tls -H tcp://testsshasm.cloudapp.net:2376 info
    Password:
    Containers: 0
    Images: 0
    Storage Driver: devicemapper
    Pool Name: docker-8:1-131781-pool
    Pool Blocksize: 65.54 kB
    Backing Filesystem: extfs
    Data file: /dev/loop0
    Metadata file: /dev/loop1
    Data Space Used: 1.821 GB
    Data Space Total: 107.4 GB
    Data Space Available: 28 GB
    Metadata Space Used: 1.479 MB
    Metadata Space Total: 2.147 GB
    Metadata Space Available: 2.146 GB
    Udev Sync Supported: true
    Deferred Removal Enabled: false
    Data loop file: /var/lib/docker/devicemapper/devicemapper/data
    Metadata loop file: /var/lib/docker/devicemapper/devicemapper/metadata
    Library Version: 1.02.77 (2012-10-15)
    Execution Driver: native-0.2
    Logging Driver: json-file
    Kernel Version: 3.19.0-28-generic
    Operating System: Ubuntu 14.04.3 LTS
    CPUs: 1
    Total Memory: 1.637 GiB
    Name: testsshasm
    WARNING: No swap limit support

只要 toobe 確定它是所有工作，您可以檢查 hello VM hello Docker 擴充功能：

    azure vm extension get testsshasm
    info: Executing command vm extension get
    + Getting virtual machines
    data: Publisher Extension name ReferenceName Version State
    data: -------------------- --------------- ------------------------- ------- ------
    data: Microsoft.Azure.E... DockerExtension DockerExtension 1.* Enable
    info: vm extension get command OK

### <a name="docker-host-vm-authentication"></a>Docker 主機 VM 驗證
此外 toocreating hello Docker VM hello`azure vm docker create`命令也會自動建立 hello 必要的憑證 tooallow Docker 用戶端電腦 tooconnect toohello Azure 容器主機使用 HTTPS，和 hello 憑證儲存在兩者hello 用戶端和主機電腦，視需要。 在後續的嘗試，會重複使用 hello 現有憑證，並將其與 hello 新主機共用中。

根據預設，憑證會放在`~/.docker`，Docker 將會在連接埠上的設定的 toorun **2376年**。 如果您想要不同的通訊埠 toouse 或目錄，則您可以使用 hello 下列其中一種`azure vm docker create`命令列選項 tooconfigure，您的 Docker 容器主機 VM toouse 不同的通訊埠或不同的憑證，來連接用戶端：

```
-dp, --docker-port [port]              Port toouse for docker [2376]
-dc, --docker-cert-dir [dir]           Directory containing docker certs [.docker/]
```

hello hello 主機上的 Docker 精靈是設定為 toolisten 和驗證用戶端 hello 上的連接指定通訊埠使用 hello 憑證產生 hello`azure vm docker create`命令。 hello 用戶端電腦必須具有這些憑證 toogain 存取 toohello Docker 主機。

> [!NOTE]
> 網路的主機執行時並沒有這些憑證將會很容易遭受 tooanyone 可以 tooconnect toohello 機器。 修改 hello 預設組態之前，請確定您已了解 hello 風險 tooyour 電腦和應用程式。
> 
> 

## <a name="next-steps"></a>後續步驟
* 您已準備好 toogo toohello [Docker 使用者指南]並使用您的 Docker VM。 toocreate Docker 功能中的 VM hello 新入口網站，請參閱[toouse hello Docker VM 擴充功能以 hello 入口網站的方式]。
* hello Azure Docker VM 擴充功能也支援 Docker Compose，其在任何環境中使用宣告式 YAML 檔案 tootake 開發人員建立模型的應用程式，並產生一致的部署。 請參閱[開始使用 Docker 和撰寫 toodefine 和 Azure 虛擬機器上執行多個容器應用程式]。  

<!--Anchors-->
[Subheading 1]:#subheading-1
[Subheading 2]:#subheading-2
[Subheading 3]:#subheading-3
[Next steps]:#next-steps

[How toouse hello Docker VM Extension with Azure]:#How-to-use-the-Docker-VM-Extension-with-Azure
[Virtual Machine Extensions for Linux and Windows]:#Virtual-Machine-Extensions-For-Linux-and-Windows
[Container and Container Management Resources for Azure]:#Container-and-Container-Management-Resources-for-Azure



<!--Link references-->
[Link 1 tooanother azure.microsoft.com documentation topic]:../../virtual-machines-windows-hero-tutorial.md
[Link 2 tooanother azure.microsoft.com documentation topic]:../../../app-service-web/web-sites-custom-domain-name.md
[Link 3 tooanother azure.microsoft.com documentation topic]:../storage-whatis-account.md
[toouse hello Docker VM 擴充功能以 hello 入口網站的方式]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-portal/

[Docker 使用者指南]:https://docs.docker.com/userguide/

[開始使用 Docker 和撰寫 toodefine 和 Azure 虛擬機器上執行多個容器應用程式]:../docker-compose-quickstart.md
