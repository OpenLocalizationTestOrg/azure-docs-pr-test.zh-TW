---
title: "aaaMove 檔案從與 SCP Azure Linux Vm tooand |Microsoft 文件"
description: "安全地移動檔案 tooand 從 Linux VM 在 Azure 中使用 SCP 和 SSH 金鑰組。"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: danlep
ms.openlocfilehash: 9e4dce667aa581df74aec3d45a6ba5e52f777d1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-files-tooand-from-a-linux-vm-using-scp"></a>移動檔案 tooand 從 Linux VM 使用 SCP

本文將說明如何 toomove 檔案從您的工作站上 tooan Azure Linux VM，或從 Azure Linux VM 關閉 tooyour 工作站上，使用安全複製 (SCP)。 在您的工作站與 Linux VM 之間快速又安全地移動檔案，對於管理您的 Azure 基礎結構來說相當重要。 

針對本文，您需要一個使用 [SSH 公開和私密金鑰檔案](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)在 Azure 中部署的 Linux VM。 此外，還需要一個用於您本機電腦的 SCP 用戶端。 它是之上 SSH，而且包含在大部分的 Linux 和 Mac 電腦和一些 Windows 殼層 hello 預設 Bash 殼層。

## <a name="quick-commands"></a>快速命令

複製 toohello Linux VM 上的檔案

```bash
scp file azureuser@azurehost:directory/targetfile
```

從 hello Linux VM，向下複製檔案

```bash
scp azureuser@azurehost:directory/file targetfile
```

## <a name="detailed-walkthrough"></a>詳細的逐步解說

做為範例，我們移動 tooa Linux VM 上的 Azure 組態檔，並提取的記錄檔目錄，同時使用 SCP 和 SSH 金鑰。   

## <a name="ssh-key-pair-authentication"></a>SSH 金鑰組驗證

SCP hello 傳輸層使用 SSH。 SSH 控點 hello hello 目的地主機上，驗證並移動透過 SSH 預設提供的加密通道中的 hello 檔案。 針對 SSH 驗證，可以使用使用者名稱和密碼。 不過，建議的安全性最佳做法是使用 SSH 公用和私密金鑰驗證。 SSH 驗證 hello 連接，一旦 SCP，就會開始將 hello 檔案複製。 使用已正確設定`~/.ssh/config`和 SSH 公用和私用索引鍵，hello SCP 連線可以建立只使用伺服器名稱 （或 IP 位址）。 如果您只有一個 SSH 金鑰，SCP 它會以尋找 hello`~/.ssh/`目錄，並使用它的預設 toolog toohello VM 中。

如需有關設定您的 `~/.ssh/config` 和 SSH 公用與私密金鑰的詳細資訊，請參閱[建立 SSH 金鑰](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

## <a name="scp-a-file-tooa-linux-vm"></a>SCP 檔案 tooa Linux VM

Hello 第一個範例中，我們要複製 tooa 是使用的 toodeploy 自動化的 Linux VM 上的 Azure 組態檔。 由於這個檔案包含 Azure API 認證，其中包含祕密，因此安全性很重要。 提供的 SSH hello 加密的通道保護 hello hello 檔案內容。

下列命令複製 hello 本機 hello *.azure/config*檔案 tooan fqdn 的 Azure VM *myserver.eastus.cloudapp.azure.com*。 hello Azure VM 上的 hello 系統管理員使用者名稱是*azureuser*. hello 檔案是目標的 toohello */首頁/azureuser/*目錄。 請在此命令中使用您自己的值來替代。

```bash
scp ~/.azure/config azureuser@myserver.eastus.cloudapp.com:/home/azureuser/config
```

## <a name="scp-a-directory-from-a-linux-vm"></a>從 Linux VM SCP 目錄

針對此範例中，我們要複製記錄檔的目錄從 hello Linux VM 關閉 tooyour 工作站。 記錄檔可能包含也可能不包含敏感或祕密資料。 不過，使用 SCP，確保加密 hello hello 記錄檔的內容。 使用 SCP tootransfer hello 檔案是最簡單方式 tooget hello hello 記錄目錄和檔案向 tooyour 工作站，同時也會安全。

hello 下列命令會將複製檔案在 hello */首頁/azureuser/記錄檔/*目錄 hello Azure VM toohello 本機 tec_rule 位於 /tmp 目錄：

```bash
scp -r azureuser@myserver.eastus.cloudapp.com:/home/azureuser/logs/. /tmp/
```

hello `-r` cli 旗標指示中列出 hello 命令中的 hello 目錄 hello 點 SCP toorecursively 複製 hello 檔案及目錄。  請注意，hello 命令列語法也是類似 tooa`cp`複製命令。

## <a name="next-steps"></a>後續步驟

* [管理使用者、 SSH 和核取，或使用 Azure Linux Vm 上的修復磁片 hello VMAccess 擴充功能](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
