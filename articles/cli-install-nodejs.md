---
title: "aaaInstall hello Azure CLI 1.0 |Microsoft 文件"
description: "安裝的 Mac、 Linux 及 Windows toostart 使用 Azure 服務的 hello Azure CLI 1.0"
editor: 
manager: timlt
documentationcenter: 
author: squillace
services: virtual-machines-linux,virtual-network,storage,azure-resource-manager
tags: azure-resource-manager,azure-service-management
ms.assetid: bdb776c8-7a76-4f3a-887c-236b4fffee10
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: command-line-interface
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: rasquill
ms.openlocfilehash: a8cd4e38fde6e4b17a768a7caecd280cd91a70f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-hello-azure-cli-10"></a>安裝 hello Azure CLI 1.0
> [!div class="op_single_selector"]
> * [PowerShell](/powershell/azure/overview)
> * [Azure CLI 1.0](cli-install-nodejs.md)
> * [Azure CLI 2.0](/cli/azure/install-azure-cli)

> [!IMPORTANT]
> 本主題描述如何 tooinstall hello Azure CLI 1.0，這建置在 nodeJs 並支援所有的傳統部署 API 呼叫以及大量的資源管理員部署活動。 您應該使用 hello [Azure CLI 2.0](/cli/azure/overview)對於新的或預視 CLI 部署和管理。

快速安裝 hello Azure 命令列介面 (Azure CLI 1.0) toouse 一組的開放原始碼 shell 命令建立及管理 Microsoft Azure 中的資源。 您有數個選項 tooinstall 這些跨平台工具在您的電腦上：

* **npm 封裝**-執行 npm （hello 適用於 JavaScript 的封裝管理員） tooinstall hello 最新 Azure CLI 1.0 封裝您的 Linux 發行版本或作業系統上。 您的電腦上需要有 node.js 和 npm。
* **安裝程式** - 下載安裝程式以輕鬆在 Mac 或 Windows 上安裝。
* **Docker 容器**-開始使用 hello 已備妥執行 Docker 容器中的最新 CLI。 您的電腦上需要有 Docker 主機。

如需詳細的選項和背景，請參閱 hello 專案儲存機制上[GitHub](https://github.com/azure/azure-xplat-cli)。

Hello Azure CLI 1.0 安裝之後，[連接與您 Azure 訂用帳戶](xplat-cli-connect.md)和執行的 hello **azure**從命令列介面 （Bash、 終端機、 命令提示字元，等等） 的命令與 toowork您的 Azure 資源。

## <a name="option-1-install-an-npm-package"></a>選項 1：安裝 npm 套件
tooinstall hello CLI 從 npm 套件，請確定您已下載並安裝 hello[最新版的 Node.js 及 npm](https://nodejs.org/en/download/package-manager/)。 然後，執行**npm 安裝**tooinstall hello azure cli 封裝：

```bash
npm install -g azure-cli
```

在 Linux 發行版本，您可能需要 toouse **sudo** toosuccessfully 執行 hello **npm**命令，如下所示：

```bash
sudo npm install -g azure-cli
```

> [!NOTE]
> 如果您需要 tooinstall 或更新的 Node.js 及 npm Linux 發行版本或作業系統上的時，建議您安裝最新 Node.js LTS 版本 hello (4.x)。 如果您使用較舊的版本，可能會發生安裝錯誤。

如果您想要的話，下載 hello 最新的 Linux [tar 檔案][ linux-installer] hello npm 封裝在本機。 然後，如下所示安裝 hello 下載的 npm 封裝 (在 Linux 發行版本中，您可能需要 toouse **sudo**):

```bash
npm install -g <path toodownloaded tar file>
```

## <a name="option-2-use-an-installer"></a>選項 2：使用安裝程式
如果您使用 Mac 或 Windows 的電腦，就有一個 hello 遵循 CLI 安裝程式可供下載：

* [Mac OS X 安裝程式][mac-installer]
* [Windows MSI][windows-installer]

> [!TIP]
> 在 Windows 中，您也可以下載 hello [Web Platform Installer](https://go.microsoft.com/?linkid=9828653) tooinstall hello CLI。 Hello 選項 tooinstall 此安裝程式可讓其他 Azure SDK 和命令列工具，在安裝之後 hello CLI。

## <a name="option-3-use-a-docker-container"></a>選項 3：使用 Docker 容器
如果您已經設定您的電腦[Docker](https://docs.docker.com/engine/understanding-docker/)主機，您可以執行 hello Docker 容器中的最新 Azure CLI 1.0。 執行 hello 下列命令 (在 Linux 發行版本中，您可能需要 toouse **sudo**):

```bash
docker run -it microsoft/azure-cli
```

## <a name="run-azure-cli-10-commands"></a>執行 Azure CLI 1.0 命令
Hello Azure CLI 1.0 安裝之後，執行 hello **azure**命令從命令列的使用者介面 （Bash、 終端機、 命令提示字元，等等）。 例如，toorun hello [說明] 命令，請 hello 下列輸入：

```azurecli
azure help
```

> [!NOTE]
> 在某些 Linux 發行版本中，您可能會收到類似的錯誤太`/usr/bin/env: ‘node’: No such file or directory`。 此錯誤訊息是來自最近安裝在 /usr/bin/nodejs 的 Node.js。 toofix，建立符號連結太/usr/bin/節點執行此命令：

```bash
sudo ln -s /usr/bin/nodejs /usr/bin/node
```

toosee hello 版的 hello Azure CLI 1.0 安裝時，下列類型 hello:

```azurecli
azure --version
```

您現在已經準備就緒！ 所有 tooaccess 都 hello 與您自己的資源，CLI 命令 toowork [tooyour Azure 訂用帳戶連線從都 hello Azure CLI](xplat-cli-connect.md)。

> [!NOTE]
> 當您第一次使用 Azure CLI 時，您會看到訊息詢問您是否要 tooallow Microsoft toocollect 使用量資訊。 參與為自願性質。 如果您選擇 tooparticipate，您可以隨時執行停止`azure telemetry --disable`。 在任何時候，tooenable 參與執行`azure telemetry --enable`。

## <a name="update-hello-cli"></a>更新 hello CLI
Microsoft 經常發行更新的版本的 hello Azure CLI。 重新安裝 hello CLI hello 安裝程式使用適用於您的作業系統，或執行 hello 最新的 Docker 容器。 或者，如果您擁有 hello 最新版的 Node.js 及 npm 安裝，藉由輸入 hello 下列更新 (在 Linux 發行版本中，您可能需要 toouse **sudo**)。

```bash
npm update -g azure-cli
```

## <a name="enable-tab-completion"></a>啟用 TAB 鍵自動完成
針對 Mac 和 Linux 提供 CLI 命令 TAB 鍵自動完成支援。

tooenable zsh，在執行：

```bash
echo '. <(azure --completion)' >> .zshrc
```

tooenable bash，在執行：

```bash
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.bash_profile
```


## <a name="next-steps"></a>後續步驟
* [從 hello CLI tooyour Azure 訂用帳戶連線](xplat-cli-connect.md)toocreate 及管理 Azure 資源。
* 深入了解 hello Azure CLI toolearn 下載原始程式碼、 報告的問題，或參與 toohello 專案，請瀏覽 hello [hello Azure CLI 的 GitHub 儲存機制](https://github.com/azure/azure-xplat-cli)。
* 如果您有使用 Azure CLI hello 或 Azure 的相關問題，請瀏覽 hello [Azure 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting)。


[mac-installer]: http://aka.ms/mac-azure-cli
[windows-installer]: http://aka.ms/webpi-azure-cli
[linux-installer]: http://aka.ms/linux-azure-cli
[cliasm]: /cli/azure/get-started-with-az-cli2
[cliarm]: ./virtual-machines/azure-cli-arm-commands.md
