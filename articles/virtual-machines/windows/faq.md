---
title: "關於 Azure 中的 Windows Vm aaaFAQ |Microsoft 文件"
description: "提供有關使用 hello 資源管理員的模型建立的 Windows 虛擬機器的 hello 常見問題的解答 toosome。"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-management
ms.assetid: 757da816-a050-4889-a010-6f75d7978eb7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: cynthn
ms.openlocfilehash: ee366a04bda347ce2be07bde4fc6bad306cc1da9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-question-about-windows-virtual-machines"></a>Windows 虛擬機器的常見問題
本文使用 hello Resource Manager 部署模型在 Azure 中建立 Windows 虛擬機器的一些常見問題。 本主題的 hello Linux 版本，請參閱[常見問題集 Linux 虛擬機器的相關問題](../linux/faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="what-can-i-run-on-an-azure-vm"></a>我可以在 Azure VM 上執行什麼？
所有的訂閱者都可以在 Azure 虛擬機器上執行伺服器軟體。 在 Azure 中執行的 Microsoft 伺服器軟體的 hello 支援原則的相關資訊，請參閱[Microsoft server software 支援適用於 Azure 虛擬機器](https://support.microsoft.com/kb/2721672)

特定版本的 Windows 7、 Windows 8.1 和 Windows 10 為可用 tooMSDN Azure 權益訂閱者和 MSDN 開發和測試隨用隨付 」 訂閱者開發和測試工作。 如需詳細資訊 (包括指示和限制)，請參閱 [MSDN 訂閱者的 Windows 用戶端映像](http://azure.microsoft.com/blog/2014/05/29/windows-client-images-on-azure/)。 

## <a name="how-much-storage-can-i-use-with-a-virtual-machine"></a>我可以使用多少的儲存體搭配虛擬機器？
每個資料磁碟可以是 up too1 TB。 您可以使用的資料磁碟的 hello 數目取決於 hello hello 虛擬機器大小。 如需詳細資訊，請參閱 [虛擬機器的大小](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

Azure 受管理的磁碟是 hello 新和建議的磁碟儲存體的供應項目用於使用 Azure 虛擬機器永續性儲存體的資料。 每部虛擬機器可使用多部受控磁碟。 受控磁碟提供兩種耐久的儲存體選項：進階與標準受控磁碟。 如需定價資訊，請參閱[受控磁碟定價](https://azure.microsoft.com/pricing/details/managed-disks)。

Azure 儲存體帳戶也可以提供儲存體 hello 作業系統磁碟和任何資料磁碟。 每個磁碟是以分頁 Blob 方式儲存的 .vhd 檔案。 如需定價的詳細資料，請參閱 [儲存體定價詳細資料](https://azure.microsoft.com/pricing/details/storage/)。

## <a name="how-can-i-access-my-virtual-machine"></a>如何存取我的虛擬機器？
使用遠端桌面連線 (RDP) 為 Windows VM 建立遠端連線。 如需指示，請參閱[如何 tooconnect 和登入 tooan Azure 虛擬機器執行 Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 支援兩個並行連線的最大值，除非 hello 伺服器設定為遠端桌面服務工作階段主機。  

如果您有遠端桌面的問題，請參閱[疑難排解遠端桌面連線 tooa windows Azure 虛擬機器](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 

如果您熟悉 HYPER-V，您可能會尋找工具類似 tooVMConnect。 Azure 不提供類似的工具，因為不支援主控台存取 tooa 虛擬機器。

## <a name="can-i-use-hello-temporary-disk-hello-d-drive-by-default-toostore-data"></a>可以使用 hello 暫存磁碟 (d： 磁碟機預設 hello) toostore 資料嗎？
請勿使用 hello 暫存磁碟 toostore 資料。 暫存磁碟僅提供暫存空間，因此您會有遺失資料且無法復原的風險。 Hello 虛擬機器會移動 tooa 不同的主機時，就可能發生資料遺失。 調整虛擬機器的大小，更新 hello 主機或硬體失敗 hello 主機上的是一些虛擬機器可能移動的 hello 原因。

如果您需要 toouse hello d： 磁碟機代號的應用程式，您可以重新指派磁碟機代號，因此 hello 暫存磁碟會使用 d： 以外的項目。 如需指示，請參閱[hello Windows 暫存磁碟的變更 hello 磁碟機代號](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。


## <a name="how-can-i-change-hello-drive-letter-of-hello-temporary-disk"></a>如何變更 hello hello 暫存磁碟的磁碟機代號？
您可以變更 hello 所移動的 hello 分頁檔的磁碟機代號和重新指派磁碟機代號，但需要 toomake 確定您執行 hello 以特定順序的步驟。 如需指示，請參閱[hello Windows 暫存磁碟的變更 hello 磁碟機代號](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。

## <a name="can-i-add-an-existing-vm-tooan-availability-set"></a>可以加入現有的 VM tooan 可用性集嗎？
否。 如果您想可用性設定組您 VM toobe 部分，您會需要 toocreate hello VM hello 集內。 目前沒有任何方式 tooadd 之後已建立設定的 VM tooan 可用性。

## <a name="can-i-upload-a-virtual-machine-tooazure"></a>可以上傳虛擬機器 tooAzure 嗎？
是。 如需指示，請參閱[移轉內部部署 Vm tooAzure](on-prem-to-azure.md)。

## <a name="can-i-resize-hello-os-disk"></a>可調整大小 hello OS 磁碟嗎？
是。 如需指示，請參閱[tooexpand hello Azure 資源群組中的虛擬機器的作業系統磁碟機的方式](expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

## <a name="can-i-copy-or-clone-an-existing-azure-vm"></a>我是否可以複製或再製現有的 Azure VM？
是。 您可以使用受管理的映像，來建立虛擬機器的映像，然後使用多個新的 Vm hello 映像 toobuild 項目。 如需指示，請參閱[建立 VM 的自訂映像](tutorial-custom-images.md)。

## <a name="why-am-i-not-seeing-canada-central-and-canada-east-regions-through-azure-resource-manager"></a>為什麼我在 Azure Resource Manager 中沒看到加拿大中部和加拿大東部區域？

hello 兩個新的區域加拿大中央和加拿大東部不會自動註冊現有的 Azure 訂用帳戶建立的虛擬機器。 透過部署虛擬機器時自動完成此項登錄 hello Azure 入口網站 tooany 使用 Azure 資源管理員的其他區域。 虛擬機器後是已部署的 tooany 其他 Azure 地區，hello 新區域應該可用於後續的虛擬機器。

## <a name="does-azure-support-linux-vms"></a>Azure 是否支援 Linux VM？
是。 tooquickly 建立時，請參閱 Linux VM tootry[使用 hello 入口網站在 Azure 上建立 Linux VM](../linux/quick-create-portal.md)。

## <a name="can-i-add-a-nic-toomy-vm-after-its-created"></a>會在建立之後可以加入 NIC toomy VM 嗎？
是的，目前可行。 hello VM 第一個需求 toobe 停止取消配置。 然後您可以新增或移除 NIC (除非它是 hello hello VM 上的最後一個 NIC)。 

## <a name="are-there-any-computer-name-requirements"></a>是否有任何電腦名稱需求？
是。 hello 電腦名稱可以是最多 15 個字元長度。 如需命名資源相關詳細資訊，請參閱[命名慣例規則與限制](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

## <a name="are-there-any-resource-group-name-requirements"></a>是否有任何資源群組名稱需求？
是。 hello 資源群組名稱可以是 90 中的字元長度最多。 如需資源群組相關詳細資訊，請參閱[命名慣例規則與限制](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

## <a name="what-are-hello-username-requirements-when-creating-a-vm"></a>建立 VM 時，有哪些 hello username 需求？

使用者名稱長度最多為 20 個字元，而且不能以句號 (".") 結尾。 


不允許下列使用者名稱的 hello:
<table>
    <tr>
        <td style="text-align:center">administrator </td><td style="text-align:center"> admin </td><td style="text-align:center"> user </td><td style="text-align:center"> user1</td>
    </tr>
    <tr>
        <td style="text-align:center">test </td><td style="text-align:center"> user2 </td><td style="text-align:center"> test1 </td><td style="text-align:center"> user3</td>
    </tr>    <tr>
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
密碼必須是長度為 12-123 個字元，且符合 3 超出 hello 下列 4 的複雜性需求：

* 包含小寫字元
* 包含大小字元
* 包含數字
* 包含特殊字元 (Regex match [\W_])

不允許 hello 下列密碼：

<table>
    <tr>
        <td>abc@123 </td>
        <td>P@$$w0rd </td>
        <td>P@ssw0rd </td>
        <td>P@ssword123 </td>
        <td>Pa$$word </td>
    </tr>
    <tr>
        <td>pass@word1 </td>
        <td>Password! </td>
        <td>Password1 </td>
        <td>Password22 </td>
        <td>iloveyou! </td>
    </tr>
</table>
