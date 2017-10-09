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
# <a name="how-tooreset-a-linux-vm-password-or-ssh-key-fix-hello-ssh-configuration-and-check-disk-consistency-using-hello-vmaccess-extension"></a><span data-ttu-id="cda44-103">如何 tooreset Linux VM 密碼或 SSH 金鑰修正 hello SSH 設定，並檢查磁碟的一致性使用 hello VMAccess 擴充功能</span><span class="sxs-lookup"><span data-stu-id="cda44-103">How tooreset a Linux VM password or SSH key, fix hello SSH configuration, and check disk consistency using hello VMAccess extension</span></span>
<span data-ttu-id="cda44-104">如果因為忘記的密碼、 不正確的安全殼層 (SSH) 金鑰或 hello SSH 組態有問題，您無法連接 tooa Linux 虛擬機器，在 Azure 上，使用與 hello Azure CLI tooreset hello 密碼或 SSH 金鑰的 hello VMAccessForLinux 延伸模組，請修正hello SSH 設定，並檢查磁碟的一致性。</span><span class="sxs-lookup"><span data-stu-id="cda44-104">If you can't connect tooa Linux virtual machine on Azure because of a forgotten password, an incorrect Secure Shell (SSH) key, or a problem with hello SSH configuration, use hello VMAccessForLinux extension with hello Azure CLI tooreset hello password or SSH key, fix hello SSH configuration, and check disk consistency.</span></span> 

> [!IMPORTANT] 
> <span data-ttu-id="cda44-105">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="cda44-105">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="cda44-106">本文件涵蓋使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="cda44-106">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="cda44-107">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="cda44-107">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="cda44-108">了解如何太[使用 hello 資源管理員的模型執行這些步驟](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess)。</span><span class="sxs-lookup"><span data-stu-id="cda44-108">Learn how too[perform these steps using hello Resource Manager model](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span></span>

<span data-ttu-id="cda44-109">Hello Azure CLI，您使用 hello **azure vm 延伸模組集**命令從命令列介面 （Bash，終端機，命令提示字元） tooaccess 命令。</span><span class="sxs-lookup"><span data-stu-id="cda44-109">With hello Azure CLI, you use hello **azure vm extension set** command from your command-line interface (Bash, Terminal, Command prompt) tooaccess commands.</span></span> <span data-ttu-id="cda44-110">如需詳細的擴充功能使用方式，請執行 **azure help vm extension set**。</span><span class="sxs-lookup"><span data-stu-id="cda44-110">Run **azure help vm extension set** for detailed extension usage.</span></span>

<span data-ttu-id="cda44-111">您可以使用 hello Azure CLI，進行下列工作 hello:</span><span class="sxs-lookup"><span data-stu-id="cda44-111">With hello Azure CLI, you can do hello following tasks:</span></span>

* [<span data-ttu-id="cda44-112">重設 hello 密碼</span><span class="sxs-lookup"><span data-stu-id="cda44-112">Reset hello password</span></span>](#pwresetcli)
* [<span data-ttu-id="cda44-113">重設 hello SSH 金鑰</span><span class="sxs-lookup"><span data-stu-id="cda44-113">Reset hello SSH key</span></span>](#sshkeyresetcli)
* [<span data-ttu-id="cda44-114">重設 hello 密碼和 hello SSH 金鑰</span><span class="sxs-lookup"><span data-stu-id="cda44-114">Reset hello password and hello SSH key</span></span>](#resetbothcli)
* [<span data-ttu-id="cda44-115">建立新的 sudo 使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="cda44-115">Create a new sudo user account</span></span>](#createnewsudocli)
* [<span data-ttu-id="cda44-116">重設 hello SSH 設定</span><span class="sxs-lookup"><span data-stu-id="cda44-116">Reset hello SSH configuration</span></span>](#sshconfigresetcli)
* [<span data-ttu-id="cda44-117">刪除使用者</span><span class="sxs-lookup"><span data-stu-id="cda44-117">Delete a user</span></span>](#deletecli)
* [<span data-ttu-id="cda44-118">顯示 hello hello VMAccess 擴充功能狀態</span><span class="sxs-lookup"><span data-stu-id="cda44-118">Display hello status of hello VMAccess extension</span></span>](#statuscli)
* [<span data-ttu-id="cda44-119">檢查新增的磁碟的一致性</span><span class="sxs-lookup"><span data-stu-id="cda44-119">Check consistency of added disks</span></span>](#checkdisk)
* [<span data-ttu-id="cda44-120">修復 Linux VM 上新增的磁碟</span><span class="sxs-lookup"><span data-stu-id="cda44-120">Repair added disks on your Linux VM</span></span>](#repairdisk)

## <a name="prerequisites"></a><span data-ttu-id="cda44-121">必要條件</span><span class="sxs-lookup"><span data-stu-id="cda44-121">Prerequisites</span></span>
<span data-ttu-id="cda44-122">您將需要 toodo hello 下列：</span><span class="sxs-lookup"><span data-stu-id="cda44-122">You will need toodo hello following:</span></span>

* <span data-ttu-id="cda44-123">您必須太[安裝 hello Azure CLI](../../../cli-install-nodejs.md)和[連接 tooyour 訂閱](../../../xplat-cli-connect.md)toouse Azure 與您的帳戶相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="cda44-123">You will need too[install hello Azure CLI](../../../cli-install-nodejs.md) and [connect tooyour subscription](../../../xplat-cli-connect.md) toouse Azure resources associated with your account.</span></span>
* <span data-ttu-id="cda44-124">在 hello 命令提示字元中輸入 hello 下列設定 hello hello 傳統部署模型的正確模式：</span><span class="sxs-lookup"><span data-stu-id="cda44-124">Set hello correct mode for hello classic deployment model by typing hello following at hello command prompt:</span></span>
    ``` 
        azure config mode asm
    ```
* <span data-ttu-id="cda44-125">有新的密碼或 SSH 金鑰組，如果您想 tooreset 其中一個。</span><span class="sxs-lookup"><span data-stu-id="cda44-125">Have a new password or set of SSH keys, if you want tooreset either one.</span></span> <span data-ttu-id="cda44-126">如果您想要 tooreset hello SSH 設定，您不需要這些。</span><span class="sxs-lookup"><span data-stu-id="cda44-126">You don't need these if you want tooreset hello SSH configuration.</span></span>

## <span data-ttu-id="cda44-127"><a name="pwresetcli"></a>重設 hello 密碼</span><span class="sxs-lookup"><span data-stu-id="cda44-127"><a name="pwresetcli"></a>Reset hello password</span></span>
1. <span data-ttu-id="cda44-128">使用下列程式行在本機電腦上建立名為 PrivateConf.json 的檔案。</span><span class="sxs-lookup"><span data-stu-id="cda44-128">Create a file on your local computer named PrivateConf.json with these lines.</span></span> <span data-ttu-id="cda44-129">以您自己的使用者名稱和密碼取代 **myUserName** 和 **myP@ssW0rd**，並設定自己的到期日期。</span><span class="sxs-lookup"><span data-stu-id="cda44-129">Replace **myUserName** and **myP@ssW0rd** with your own user name and password and set your own date for expiration.</span></span>

    ```   
        {
        "username":"myUserName",
        "password":"myP@ssW0rd",
        "expiration":"2020-01-01"
        }
    ```
        
2. <span data-ttu-id="cda44-130">執行此命令，並以您的虛擬機器的 hello 名稱取代**myVM**。</span><span class="sxs-lookup"><span data-stu-id="cda44-130">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* –-private-config-path PrivateConf.json
    ```

## <span data-ttu-id="cda44-131"><a name="sshkeyresetcli"></a>重設 hello SSH 金鑰</span><span class="sxs-lookup"><span data-stu-id="cda44-131"><a name="sshkeyresetcli"></a>Reset hello SSH key</span></span>
1. <span data-ttu-id="cda44-132">使用下列內容建立名為 PrivateConf.json 的檔案。</span><span class="sxs-lookup"><span data-stu-id="cda44-132">Create a file named PrivateConf.json with these contents.</span></span> <span data-ttu-id="cda44-133">取代 hello **myUserName**和**mySSHKey**具有您個人資訊的值。</span><span class="sxs-lookup"><span data-stu-id="cda44-133">Replace hello **myUserName** and **mySSHKey** values with your own information.</span></span>

    ```   
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey"
        }
    ```
2. <span data-ttu-id="cda44-134">執行此命令，並以您的虛擬機器的 hello 名稱取代**myVM**。</span><span class="sxs-lookup"><span data-stu-id="cda44-134">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span>
   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json

## <span data-ttu-id="cda44-135"><a name="resetbothcli"></a>重設密碼 hello 與 hello SSH 金鑰</span><span class="sxs-lookup"><span data-stu-id="cda44-135"><a name="resetbothcli"></a>Reset both hello password and hello SSH key</span></span>
1. <span data-ttu-id="cda44-136">使用下列內容建立名為 PrivateConf.json 的檔案。</span><span class="sxs-lookup"><span data-stu-id="cda44-136">Create a file named PrivateConf.json with these contents.</span></span> <span data-ttu-id="cda44-137">取代 hello **myUserName**， **mySSHKey**和 **myP@ssW0rd** 具有您個人資訊的值。</span><span class="sxs-lookup"><span data-stu-id="cda44-137">Replace hello **myUserName**, **mySSHKey** and **myP@ssW0rd** values with your own information.</span></span>

    ``` 
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey",
        "password":"myP@ssW0rd"
        }
    ```

2. <span data-ttu-id="cda44-138">執行此命令，並以您的虛擬機器的 hello 名稱取代**myVM**。</span><span class="sxs-lookup"><span data-stu-id="cda44-138">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set MyVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <span data-ttu-id="cda44-139"><a name="createnewsudocli"></a>建立新的 sudo 使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="cda44-139"><a name="createnewsudocli"></a>Create a new sudo user account</span></span>

<span data-ttu-id="cda44-140">如果您忘記您的使用者名稱，您可以使用 VMAccess toocreate 一個新 hello sudo 授權單位。</span><span class="sxs-lookup"><span data-stu-id="cda44-140">If you forget your user name, you can use VMAccess toocreate a new one with hello sudo authority.</span></span> <span data-ttu-id="cda44-141">在此情況下，hello 現有的使用者名稱和密碼將不會修改。</span><span class="sxs-lookup"><span data-stu-id="cda44-141">In this case, hello existing user name and password will not be modified.</span></span>

<span data-ttu-id="cda44-142">toocreate 新 sudo 使用者與密碼存取、 使用中的 hello 指令碼[重設 hello 密碼](#pwresetcli)並指定 hello 新的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="cda44-142">toocreate a new sudo user with password access, use hello script in [Reset hello password](#pwresetcli) and specify hello new user name.</span></span>

<span data-ttu-id="cda44-143">SSH 金鑰的存取，使用 hello 指令碼中使用新的 sudo 使用者 toocreate[重設 hello SSH 金鑰](#sshkeyresetcli)並指定 hello 新的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="cda44-143">toocreate a new sudo user with SSH key access, use hello script in [Reset hello SSH key](#sshkeyresetcli) and specify hello new user name.</span></span>

<span data-ttu-id="cda44-144">您也可以使用[重設 hello 密碼與 hello SSH 金鑰](#resetbothcli)toocreate 之新使用者的密碼和 SSH 金鑰的存取。</span><span class="sxs-lookup"><span data-stu-id="cda44-144">You can also use [Reset hello password and hello SSH key](#resetbothcli) toocreate a new user with both password and SSH key access.</span></span>

## <span data-ttu-id="cda44-145"><a name="sshconfigresetcli"></a>重設 hello SSH 設定</span><span class="sxs-lookup"><span data-stu-id="cda44-145"><a name="sshconfigresetcli"></a>Reset hello SSH configuration</span></span>
<span data-ttu-id="cda44-146">如果 hello SSH 組態處於不良狀態，也可能會遺失存取 toohello VM。</span><span class="sxs-lookup"><span data-stu-id="cda44-146">If hello SSH configuration is in an undesired state, you might also lose access toohello VM.</span></span> <span data-ttu-id="cda44-147">您可以使用 hello VMAccess 擴充功能 tooreset hello 組態 tooits 預設狀態。</span><span class="sxs-lookup"><span data-stu-id="cda44-147">You can use hello VMAccess extension tooreset hello configuration tooits default state.</span></span> <span data-ttu-id="cda44-148">toodo 因此，您只需要 tooset hello"reset_ssh"索引鍵太"True"。</span><span class="sxs-lookup"><span data-stu-id="cda44-148">toodo so, you just need tooset hello “reset_ssh” key too“True”.</span></span> <span data-ttu-id="cda44-149">hello 延伸模組會重新啟動 hello SSH 伺服器、 開啟您的 VM 上的 hello SSH 連接埠和 hello SSH 組態 toodefault 值重設。</span><span class="sxs-lookup"><span data-stu-id="cda44-149">hello extension will restart hello SSH server, open hello SSH port on your VM, and reset hello SSH configuration toodefault values.</span></span> <span data-ttu-id="cda44-150">不會變更 hello 使用者帳戶 （名稱、 密碼或 SSH 金鑰）。</span><span class="sxs-lookup"><span data-stu-id="cda44-150">hello user account (name, password or SSH keys) will not be changed.</span></span>

> [!NOTE]
> <span data-ttu-id="cda44-151">取得重設的 hello SSH 組態檔位於 /etc/ssh/sshd_config。</span><span class="sxs-lookup"><span data-stu-id="cda44-151">hello SSH configuration file that gets reset is located at /etc/ssh/sshd_config.</span></span>
> 
> 

1. <span data-ttu-id="cda44-152">使用此內容建立名為 PrivateConf.json 的檔案。</span><span class="sxs-lookup"><span data-stu-id="cda44-152">Create a file named PrivateConf.json with this content.</span></span>

    ```   
        {
        "reset_ssh":"True"
        }
    ```

2. <span data-ttu-id="cda44-153">執行此命令，並以您的虛擬機器的 hello 名稱取代**myVM**。</span><span class="sxs-lookup"><span data-stu-id="cda44-153">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span> 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <span data-ttu-id="cda44-154"><a name="deletecli"></a>刪除使用者</span><span class="sxs-lookup"><span data-stu-id="cda44-154"><a name="deletecli"></a>Delete a user</span></span>
<span data-ttu-id="cda44-155">如果您想 toodelete 沒有直接登入 toohello VM 的使用者帳戶，您可以使用這個指令碼。</span><span class="sxs-lookup"><span data-stu-id="cda44-155">If you want toodelete a user account without logging into toohello VM directly, you can use this script.</span></span>

1. <span data-ttu-id="cda44-156">建立名為此內容，以替代的 hello 使用者名稱 tooremove 的 PrivateConf.json **removeUserName**。</span><span class="sxs-lookup"><span data-stu-id="cda44-156">Create a file named PrivateConf.json with this content, substituting hello user name tooremove for **removeUserName**.</span></span> 

    ```   
        {
        "remove_user":"removeUserName"
        }
    ```

2. <span data-ttu-id="cda44-157">執行此命令，並以您的虛擬機器的 hello 名稱取代**myVM**。</span><span class="sxs-lookup"><span data-stu-id="cda44-157">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span> 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <span data-ttu-id="cda44-158"><a name="statuscli"></a>顯示 hello hello VMAccess 擴充功能狀態</span><span class="sxs-lookup"><span data-stu-id="cda44-158"><a name="statuscli"></a>Display hello status of hello VMAccess extension</span></span>
<span data-ttu-id="cda44-159">toodisplay hello 狀態 hello VMAccess 擴充功能，執行此命令。</span><span class="sxs-lookup"><span data-stu-id="cda44-159">toodisplay hello status of hello VMAccess extension, run this command.</span></span>

```
        azure vm extension get
```

## <span data-ttu-id="cda44-160"><a name='checkdisk'></a>檢查新增的磁碟的一致性</span><span class="sxs-lookup"><span data-stu-id="cda44-160"><a name='checkdisk'></a>Check consistency of added disks</span></span>
<span data-ttu-id="cda44-161">toorun fsck Linux 虛擬機器中的所有磁碟上，您將需要 toodo hello 下列：</span><span class="sxs-lookup"><span data-stu-id="cda44-161">toorun fsck on all disks in your Linux virtual machine, you will need toodo hello following:</span></span>

1. <span data-ttu-id="cda44-162">使用此內容建立名為 PublicConf.json 的檔案。</span><span class="sxs-lookup"><span data-stu-id="cda44-162">Create a file named PublicConf.json with this content.</span></span> <span data-ttu-id="cda44-163">請檢查磁碟所需的布林值 toocheck 磁碟是否附加 tooyour 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="cda44-163">Check Disk takes a boolean for whether toocheck disks attached tooyour virtual machine or not.</span></span> 

    ```   
        {   
        "check_disk": "true"
        }
    ```

2. <span data-ttu-id="cda44-164">執行這個命令 tooexecute，並以您的虛擬機器的 hello 名稱取代**myVM**。</span><span class="sxs-lookup"><span data-stu-id="cda44-164">Run this command tooexecute, substituting hello name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json 
    ```

## <span data-ttu-id="cda44-165"><a name='repairdisk'></a>修復磁碟</span><span class="sxs-lookup"><span data-stu-id="cda44-165"><a name='repairdisk'></a>Repair disks</span></span>
<span data-ttu-id="cda44-166">無法裝載或已掛接組態錯誤，請使用您的 Linux 虛擬機器上的 hello VMAccess 擴充功能 tooreset hello 掛接組態 toorepair 磁碟。</span><span class="sxs-lookup"><span data-stu-id="cda44-166">toorepair disks that are not mounting or have mount configuration errors, use hello VMAccess extension tooreset hello mount configuration on your Linux virtual machine.</span></span> <span data-ttu-id="cda44-167">取代為您磁碟 hello 名稱**myDisk**。</span><span class="sxs-lookup"><span data-stu-id="cda44-167">Substituting hello name of your disk for **myDisk**.</span></span>

1. <span data-ttu-id="cda44-168">使用此內容建立名為 PublicConf.json 的檔案。</span><span class="sxs-lookup"><span data-stu-id="cda44-168">Create a file named PublicConf.json with this content.</span></span> 

    ```   
        {
        "repair_disk":"true",
        "disk_name":"myDisk"
        }
    ```

2. <span data-ttu-id="cda44-169">執行這個命令 tooexecute，並以您的虛擬機器的 hello 名稱取代**myVM**。</span><span class="sxs-lookup"><span data-stu-id="cda44-169">Run this command tooexecute, substituting hello name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json
    ```

## <a name="next-steps"></a><span data-ttu-id="cda44-170">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cda44-170">Next steps</span></span>
* <span data-ttu-id="cda44-171">如果您想 toouse Azure PowerShell cmdlet 或 Azure 資源管理員範本 tooreset hello 密碼或 SSH 金鑰，修正 hello SSH 設定，並檢查磁碟的一致性，請參閱 hello [VMAccess 擴充功能的文件 GitHub 上](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess)。</span><span class="sxs-lookup"><span data-stu-id="cda44-171">If you want toouse Azure PowerShell cmdlets or Azure Resource Manager templates tooreset hello password or SSH key, fix hello SSH configuration, and check disk consistency, see hello [VMAccess extension documentation on GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span></span> 
* <span data-ttu-id="cda44-172">您也可以使用 hello [Azure 入口網站](https://portal.azure.com)tooreset hello 密碼或 SSH 金鑰的 Linux VM 部署在 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="cda44-172">You can also use hello [Azure portal](https://portal.azure.com) tooreset hello password or SSH key of a Linux VM deployed in hello classic deployment model.</span></span> <span data-ttu-id="cda44-173">您目前無法使用 hello 入口網站執行 toothis Linux VM 部署在 hello Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="cda44-173">You can't currently use hello portal do toothis for a Linux VM deployed in hello Resource Manager deployment model.</span></span>
* <span data-ttu-id="cda44-174">如需使用 Azure 虛擬機器 VM 擴充功能的詳細資訊，請參閱[有關虛擬機器擴充功能和功能](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="cda44-174">See [About virtual machine extensions and features](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more about using VM extensions for Azure virtual machines.</span></span>

