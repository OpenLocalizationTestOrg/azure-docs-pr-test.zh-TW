---
title: "aaaReset Linux VM 的密碼和 SSH 金鑰從 hello CLI |Microsoft 文件"
description: "Toouse hello VMAccess 擴充功能，從 hello Azure 命令列介面 (CLI) tooreset Linux VM 密碼或 SSH 金鑰如何修正 hello SSH 設定，並檢查磁碟的一致性"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: d975eb70-5ff1-40d1-a634-8dd2646dcd17
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: cynthn
ms.openlocfilehash: 1650ad64fb982627ae9f90b1a8209bb56bac7004
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-a-linux-vm-password-or-ssh-key-fix-hello-ssh-configuration-and-check-disk-consistency-using-hello-vmaccess-extension"></a>如何 tooreset Linux VM 密碼或 SSH 金鑰修正 hello SSH 設定，並檢查磁碟的一致性使用 hello VMAccess 擴充功能
如果因為忘記的密碼、 不正確的安全殼層 (SSH) 金鑰或 hello SSH 組態有問題，您無法連接 tooa Linux 虛擬機器，在 Azure 上，使用與 hello Azure CLI tooreset hello 密碼或 SSH 金鑰的 hello VMAccessForLinux 延伸模組，請修正hello SSH 設定，並檢查磁碟的一致性。 

> [!IMPORTANT] 
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。 本文件涵蓋使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。 了解如何太[使用 hello 資源管理員的模型執行這些步驟](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess)。

Hello Azure CLI，您使用 hello **azure vm 延伸模組集**命令從命令列介面 （Bash，終端機，命令提示字元） tooaccess 命令。 如需詳細的擴充功能使用方式，請執行 **azure help vm extension set**。

您可以使用 hello Azure CLI，進行下列工作 hello:

* [重設 hello 密碼](#pwresetcli)
* [重設 hello SSH 金鑰](#sshkeyresetcli)
* [重設 hello 密碼和 hello SSH 金鑰](#resetbothcli)
* [建立新的 sudo 使用者帳戶](#createnewsudocli)
* [重設 hello SSH 設定](#sshconfigresetcli)
* [刪除使用者](#deletecli)
* [顯示 hello hello VMAccess 擴充功能狀態](#statuscli)
* [檢查新增的磁碟的一致性](#checkdisk)
* [修復 Linux VM 上新增的磁碟](#repairdisk)

## <a name="prerequisites"></a>必要條件
您將需要 toodo hello 下列：

* 您必須太[安裝 hello Azure CLI](../../../cli-install-nodejs.md)和[連接 tooyour 訂閱](../../../xplat-cli-connect.md)toouse Azure 與您的帳戶相關聯的資源。
* 在 hello 命令提示字元中輸入 hello 下列設定 hello hello 傳統部署模型的正確模式：
    ``` 
        azure config mode asm
    ```
* 有新的密碼或 SSH 金鑰組，如果您想 tooreset 其中一個。 如果您想要 tooreset hello SSH 設定，您不需要這些。

## <a name="pwresetcli"></a>重設 hello 密碼
1. 使用下列程式行在本機電腦上建立名為 PrivateConf.json 的檔案。 以您自己的使用者名稱和密碼取代 **myUserName** 和 **myP@ssW0rd**，並設定自己的到期日期。

    ```   
        {
        "username":"myUserName",
        "password":"myP@ssW0rd",
        "expiration":"2020-01-01"
        }
    ```
        
2. 執行此命令，並以您的虛擬機器的 hello 名稱取代**myVM**。

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* –-private-config-path PrivateConf.json
    ```

## <a name="sshkeyresetcli"></a>重設 hello SSH 金鑰
1. 使用下列內容建立名為 PrivateConf.json 的檔案。 取代 hello **myUserName**和**mySSHKey**具有您個人資訊的值。

    ```   
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey"
        }
    ```
2. 執行此命令，並以您的虛擬機器的 hello 名稱取代**myVM**。
   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json

## <a name="resetbothcli"></a>重設密碼 hello 與 hello SSH 金鑰
1. 使用下列內容建立名為 PrivateConf.json 的檔案。 取代 hello **myUserName**， **mySSHKey**和 **myP@ssW0rd** 具有您個人資訊的值。

    ``` 
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey",
        "password":"myP@ssW0rd"
        }
    ```

2. 執行此命令，並以您的虛擬機器的 hello 名稱取代**myVM**。

    ```   
        azure vm extension set MyVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <a name="createnewsudocli"></a>建立新的 sudo 使用者帳戶

如果您忘記您的使用者名稱，您可以使用 VMAccess toocreate 一個新 hello sudo 授權單位。 在此情況下，hello 現有的使用者名稱和密碼將不會修改。

toocreate 新 sudo 使用者與密碼存取、 使用中的 hello 指令碼[重設 hello 密碼](#pwresetcli)並指定 hello 新的使用者名稱。

SSH 金鑰的存取，使用 hello 指令碼中使用新的 sudo 使用者 toocreate[重設 hello SSH 金鑰](#sshkeyresetcli)並指定 hello 新的使用者名稱。

您也可以使用[重設 hello 密碼與 hello SSH 金鑰](#resetbothcli)toocreate 之新使用者的密碼和 SSH 金鑰的存取。

## <a name="sshconfigresetcli"></a>重設 hello SSH 設定
如果 hello SSH 組態處於不良狀態，也可能會遺失存取 toohello VM。 您可以使用 hello VMAccess 擴充功能 tooreset hello 組態 tooits 預設狀態。 toodo 因此，您只需要 tooset hello"reset_ssh"索引鍵太"True"。 hello 延伸模組會重新啟動 hello SSH 伺服器、 開啟您的 VM 上的 hello SSH 連接埠和 hello SSH 組態 toodefault 值重設。 不會變更 hello 使用者帳戶 （名稱、 密碼或 SSH 金鑰）。

> [!NOTE]
> 取得重設的 hello SSH 組態檔位於 /etc/ssh/sshd_config。
> 
> 

1. 使用此內容建立名為 PrivateConf.json 的檔案。

    ```   
        {
        "reset_ssh":"True"
        }
    ```

2. 執行此命令，並以您的虛擬機器的 hello 名稱取代**myVM**。 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <a name="deletecli"></a>刪除使用者
如果您想 toodelete 沒有直接登入 toohello VM 的使用者帳戶，您可以使用這個指令碼。

1. 建立名為此內容，以替代的 hello 使用者名稱 tooremove 的 PrivateConf.json **removeUserName**。 

    ```   
        {
        "remove_user":"removeUserName"
        }
    ```

2. 執行此命令，並以您的虛擬機器的 hello 名稱取代**myVM**。 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <a name="statuscli"></a>顯示 hello hello VMAccess 擴充功能狀態
toodisplay hello 狀態 hello VMAccess 擴充功能，執行此命令。

```
        azure vm extension get
```

## <a name='checkdisk'></a>檢查新增的磁碟的一致性
toorun fsck Linux 虛擬機器中的所有磁碟上，您將需要 toodo hello 下列：

1. 使用此內容建立名為 PublicConf.json 的檔案。 請檢查磁碟所需的布林值 toocheck 磁碟是否附加 tooyour 虛擬機器。 

    ```   
        {   
        "check_disk": "true"
        }
    ```

2. 執行這個命令 tooexecute，並以您的虛擬機器的 hello 名稱取代**myVM**。

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json 
    ```

## <a name='repairdisk'></a>修復磁碟
無法裝載或已掛接組態錯誤，請使用您的 Linux 虛擬機器上的 hello VMAccess 擴充功能 tooreset hello 掛接組態 toorepair 磁碟。 取代為您磁碟 hello 名稱**myDisk**。

1. 使用此內容建立名為 PublicConf.json 的檔案。 

    ```   
        {
        "repair_disk":"true",
        "disk_name":"myDisk"
        }
    ```

2. 執行這個命令 tooexecute，並以您的虛擬機器的 hello 名稱取代**myVM**。

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json
    ```

## <a name="next-steps"></a>後續步驟
* 如果您想 toouse Azure PowerShell cmdlet 或 Azure 資源管理員範本 tooreset hello 密碼或 SSH 金鑰，修正 hello SSH 設定，並檢查磁碟的一致性，請參閱 hello [VMAccess 擴充功能的文件 GitHub 上](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess)。 
* 您也可以使用 hello [Azure 入口網站](https://portal.azure.com)tooreset hello 密碼或 SSH 金鑰的 Linux VM 部署在 hello 傳統部署模型。 您目前無法使用 hello 入口網站執行 toothis Linux VM 部署在 hello Resource Manager 部署模型。
* 如需使用 Azure 虛擬機器 VM 擴充功能的詳細資訊，請參閱[有關虛擬機器擴充功能和功能](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

