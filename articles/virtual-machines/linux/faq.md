---
title: "適用於 Linux Vm 在 Azure 中的常見問題 aaaFrequently |Microsoft 文件"
description: "提供有關使用 hello 資源管理員的模型建立的 Linux 虛擬機器的 hello 常見問題的解答 toosome。"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-management
ms.assetid: 3648e09c-1115-4818-93c6-688d7a54a353
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: cynthn
ms.openlocfilehash: 0afd08123dddc408851065c46deedc3146dbec20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-question-about-linux-virtual-machines"></a>Linux 虛擬機器的常見問題
本文使用 hello Resource Manager 部署模型在 Azure 中建立的 Linux 虛擬機器的一些常見問題。 本主題的 hello Windows 版本，請參閱[常見問題集有關 Windows 虛擬機器的問題](../windows/faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="what-can-i-run-on-an-azure-vm"></a>我可以在 Azure VM 上執行什麼？
所有的訂閱者都可以在 Azure 虛擬機器上執行伺服器軟體。 如需詳細資訊，請參閱 [經 Azure 背書之配送映像上的 Linux](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="how-much-storage-can-i-use-with-a-virtual-machine"></a>我可以使用多少的儲存體搭配虛擬機器？
每個資料磁碟可以是 up too1 TB。 您可以使用的資料磁碟的 hello 數目取決於 hello hello 虛擬機器大小。 如需詳細資訊，請參閱 [虛擬機器的大小](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

Azure 儲存體帳戶提供 hello 作業系統磁碟和任何資料磁碟的儲存體。 每個磁碟是以分頁 Blob 方式儲存的 .vhd 檔案。 如需定價的詳細資料，請參閱 [儲存體定價詳細資料](https://azure.microsoft.com/pricing/details/storage/)。

## <a name="how-can-i-access-my-virtual-machine"></a>如何存取我的虛擬機器？
建立遠端連線 toolog toohello 虛擬機器上，使用安全殼層 (SSH)。 請參閱如何 hello 指示 tooconnect[從 Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)或[從 Linux 和 Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。 根據預設，SSH 允許最多 10 個並行連線。 您可以增加這個數字藉由編輯 hello 設定檔。

如果您遇到問題，請參閱 [疑難排解以 Linux 為基礎之 Azure 虛擬機器的安全殼層 (SSH) 連線](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

## <a name="can-i-use-hello-temporary-disk-devsdb1-toostore-data"></a>可以使用 hello 暫存磁碟 (/ 開發/sdb1) toostore 資料嗎？
請勿使用 hello 暫存磁碟 (/ 開發/sdb1) toostore 資料。 它只是用於暫時儲存。 您可能會遺失資料且無法復原。

## <a name="can-i-copy-or-clone-an-existing-azure-vm"></a>我是否可以複製或再製現有的 Azure VM？
是。 如需指示，請參閱[toocreate Linux 虛擬機器中的 hello Resource Manager 部署模型的方式](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

## <a name="why-am-i-not-seeing-canada-central-and-canada-east-regions-through-azure-resource-manager"></a>為什麼我在 Azure Resource Manager 中沒看到加拿大中部和加拿大東部區域？
hello 兩個新的區域加拿大中央和加拿大東部不會自動註冊現有的 Azure 訂用帳戶建立的虛擬機器。 透過部署虛擬機器時自動完成此項登錄 hello Azure 入口網站 tooany 使用 Azure 資源管理員的其他區域。 虛擬機器後是已部署的 tooany 其他 Azure 地區，hello 新區域應該可用於後續的虛擬機器。

## <a name="can-i-add-a-nic-toomy-vm-after-its-created"></a>會在建立之後可以加入 NIC toomy VM 嗎？
是的，目前可行。 hello VM 第一個需求 toobe 停止取消配置。 然後您可以新增或移除 NIC (除非它是 hello hello VM 上的最後一個 NIC)。 

## <a name="are-there-any-computer-name-requirements"></a>是否有任何電腦名稱需求？
是。 hello 電腦名稱可以是最多 64 個字元的長度。 如需命名資源相關詳細資訊，請參閱[命名慣例規則與限制](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

## <a name="are-there-any-resource-group-name-requirements"></a>是否有任何資源群組名稱需求？
是。 hello 資源群組名稱可以是 90 中的字元長度最多。 如需資源群組相關詳細資訊，請參閱[命名慣例規則與限制](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

## <a name="what-are-hello-username-requirements-when-creating-a-vm"></a>建立 VM 時，有哪些 hello username 需求？
使用者名稱必須是長度在 1 - 64 之間的字元。

不允許下列使用者名稱的 hello:

<table>
    <tr>
        <td style="text-align:center">administrator </td><td style="text-align:center"> admin </td><td style="text-align:center"> user </td><td style="text-align:center"> user1</td>
    </tr>
    <tr>
        <td style="text-align:center">test </td><td style="text-align:center"> user2 </td><td style="text-align:center"> test1 </td><td style="text-align:center"> user3</td>
    </tr>
    <tr>
        <td style="text-align:center">admin1 </td><td style="text-align:center"> 1 </td><td style="text-align:center"> 123 </td><td style="text-align:center"> a</td>
    </tr>
    <tr>
        <td style="text-align:center">actuser  </td><td style="text-align:center"> adm </td><td style="text-align:center"> admin2 </td><td style="text-align:center"> aspnet</td>
    </tr>
    <tr>
        <td style="text-align:center">backup </td><td style="text-align:center"> console </td><td style="text-align:center"> david </td><td style="text-align:center"> guest</td>
    </tr>
    <tr>
        <td style="text-align:center">john </td><td style="text-align:center"> owner </td><td style="text-align:center"> root </td><td style="text-align:center"> 伺服器</td>
    </tr>
    <tr>
        <td style="text-align:center">sql </td><td style="text-align:center"> 支援 </td><td style="text-align:center"> support_388945a0 </td><td style="text-align:center"> sys</td>
    </tr>
    <tr>
        <td style="text-align:center">test2 </td><td style="text-align:center"> test3 </td><td style="text-align:center"> user4 </td><td style="text-align:center"> user5</td>
    </tr>
</table>


## <a name="what-are-hello-password-requirements-when-creating-a-vm"></a>建立 VM 時，有哪些 hello 密碼需求？
密碼必須是長度為 6 72 個字元，且符合 3 超出 hello 下列 4 的複雜性需求：

* 包含小寫字元
* 包含大小字元
* 包含數字
* 包含特殊字元 (Regex match [\W_])

不允許 hello 下列密碼：

<table>
    <tr>
        <td style="text-align:center">abc@123</td>
        <td style="text-align:center">P@$$w0rd</td>
        <td style="text-align:center">P@ssw0rd</td>
        <td style="text-align:center">P@ssword123</td>
        <td style="text-align:center">Pa$$word</td>
    </tr>
    <tr>
        <td style="text-align:center">pass@word1</td>
        <td style="text-align:center">Password!</td>
        <td style="text-align:center">Password1</td>
        <td style="text-align:center">Password22</td>
        <td style="text-align:center">iloveyou!</td>
    </tr>
</table>
