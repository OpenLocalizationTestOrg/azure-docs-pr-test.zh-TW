---
title: "aaaCreate 及使用 SSH 金鑰組適用於 Linux Vm 在 Azure 中 |Microsoft 文件"
description: "如何 toocreate，SSH 公開金鑰和私密金鑰組適用於 Linux Vm 中的使用 Azure tooimprove hello hello 驗證程序的安全性。"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 34ae9482-da3e-4b2d-9d0d-9d672aa42498
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/14/2017
ms.author: iainfou
ms.openlocfilehash: 7fb94841d34d5bc006f3134adf91102ddce5f174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-use-an-ssh-public-and-private-key-pair-for-linux-vms-in-azure"></a>適用於在 Azure 中的 Linux Vm 配對 toocreate 及使用 SSH 公用和私用金鑰的方式
使用安全殼層 (SSH) 金鑰組，您可以使用 SSH 金鑰進行驗證，免除對密碼 toolog 中的 hello 需要的 Azure 中建立虛擬機器 (Vm)。 本文章將示範如何 tooquickly 產生及使用 SSH 通訊協定第 2 版 RSA 公開金鑰和私密金鑰的金鑰檔組適用於 Linux Vm。 如需詳細步驟和其他範例，請參閱[詳細步驟 toocreate SSH 金鑰組和憑證](create-ssh-keys-detailed.md)。

## <a name="create-an-ssh-key-pair"></a>建立 SSH 金鑰組
使用 hello`ssh-keygen`命令 toocreate SSH 公開金鑰和私密金鑰檔案預設建立在 hello`~/.ssh`目錄，但您可以指定不同的位置和其他的複雜密碼 （密碼 tooaccess hello 私密金鑰檔案） 時提示您。 執行 hello Bash 殼層中的下列命令，建立回答 hello 提示與您自己的資訊。

```bash
ssh-keygen -t rsa -b 2048
```

## <a name="use-hello-ssh-key-pair"></a>使用 hello SSH 金鑰組
hello 您放在 Azure 中 Linux VM 的公用金鑰是儲存在預設`~/.ssh/id_rsa.pub`，除非您在建立時，變更 hello 位置。 如果您使用 hello [Azure CLI 2.0](/cli/azure) toocreate VM，指定此公開金鑰 hello 位置，當您使用 hello [az vm 建立](/cli/azure/vm#create)以 hello`--ssh-key-path`選項。 如果您複製並貼上 hello Azure 入口網站或資源管理員範本中的 hello 公開金鑰檔案 toouse hello 內容，請確定您沒有複製任何額外的空白字元。 例如，如果您使用 OS X，您可以使用管線傳送 hello 公開金鑰檔案 (根據預設， **~/.ssh/id_rsa.pub**) 太**pbcopy** toocopy hello 內容 （有沒有 hello 相同的事物，例如其他Linux程式`xclip`).

如果您不熟悉 SSH 公開金鑰，您可以如下所示執行 `cat`，並以您自己的公開金鑰檔案位置取代 `~/.ssh/id_rsa.pub`，來看到您的公開金鑰︰

```bash
cat ~/.ssh/id_rsa.pub
```

使用 hello Azure VM 上的公用金鑰，SSH tooyour VM 使用 hello IP 位址或 DNS 名稱的 VM (請記住 tooreplace`azureuser`和`myvm.westus.cloudapp.azure.com`底下具有 hello 管理員使用者名稱和 hello 完整的網域名稱或 IP 位址):

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

如果您在建立您的金鑰組時，您會提供複雜密碼，請輸入 hello 複雜密碼 hello 登入程序期間出現提示時。 (hello 伺服器新增 tooyour`~/.ssh/known_hosts`資料夾，而您就不會要求 tooconnect 一次，直到 hello 公開金鑰的 Azure VM 變更或移除 hello 伺服器名稱是`~/.ssh/known_hosts`。)

## <a name="next-steps"></a>後續步驟

依預設停用的密碼設定是使用 SSH 金鑰建立的 Vm，大幅更耗費資源，因此難以猜測 toomake 暴力密碼破解強制嘗試。 本主題描述如何建立簡單的 SSH 金鑰組以供快速使用。 如果您需要更多協助建立您的 SSH 金鑰組，或需要其他憑證，請參閱[詳細步驟 toocreate SSH 金鑰組和憑證](create-ssh-keys-detailed.md)。

您可以建立使用您使用 hello Azure 入口網站、 CLI 和範本的 SSH 金鑰組的 Vm:

* [建立安全的 Linux VM，使用 hello Azure 入口網站](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [建立安全的 Linux VM，使用 hello Azure CLI 2.0）](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [使用 Azure 範本建立安全的 Linux VM](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
