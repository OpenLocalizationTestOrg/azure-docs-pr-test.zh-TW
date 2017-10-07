---
title: "aaaManage Azure 端點的存取控制清單 |PowerShell |傳統 |Microsoft 文件"
description: "深入了解如何使用 PowerShell 的 Acl toomanage"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: c84e40af-f351-4572-b3f0-d572d46bafe7
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: a7ca241ea108a266085bfb689b742d781e58da1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-endpoint-access-control-lists-using-powershell-in-hello-classic-deployment-model"></a>管理端點的存取控制清單在 hello 傳統部署模型中使用 PowerShell
您可以建立和管理網路存取控制清單 (Acl) 端點使用 Azure PowerShell 或 hello 管理入口網站中。 在本主題中，您會了解一些可使用 PowerShell 完成 ACL 一般工作的程序。 Hello 清單的 Azure PowerShell cmdlet，請參閱[Azure 管理 Cmdlet](http://go.microsoft.com/fwlink/?LinkId=317721)。 如需有關 ACL 的詳細資訊，請參閱＜ [什麼是網路存取控制清單 (ACL)？](virtual-networks-acl.md)＞。 如果您想要 toomanage Acl hello 管理入口網站，請參閱[如何 tooSet 端點 tooa 虛擬機器](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。

## <a name="manage-network-acls-by-using-azure-powershell"></a>使用 Azure PowerShell 來管理網路 ACL
您可以使用 Azure PowerShell cmdlet toocreate、 移除和設定 (set) 網路存取控制清單 (Acl)。 我們包含了一些您可以設定使用 PowerShell 的 ACL 的 hello 方法的一些範例。

tooretrieve hello ACL PowerShell 指令程式的完整清單，您可以使用 hello 下列其中一項：

    Get-Help *AzureACL*
    Get-Command -Noun AzureACLConfig

### <a name="create-a-network-acl-with-rules-that-permit-access-from-a-remote-subnet"></a>建立網路 ACL 搭配規則以允許從遠端子網路進行存取
hello 下列範例所示方式 toocreate 包含規則的新 ACL。 此 ACL 隨後將套用 tooa 虛擬機器端點。 在 hello 面範例中的 hello ACL 規則將允許從遠端子網路的存取。 新的網路 ACL 對遠端子網路，允許規則與 toocreate 開啟 Azure PowerShell ISE。 複製和貼上 hello 下方，使用您自己的值，設定 hello 指令碼的指令碼，然後執行 hello 指令碼。

1. 建立 hello 新的網路 ACL 物件。
   
        $acl1 = New-AzureAclConfig
2. 設定規則以允許從遠端子網路進行存取。 在 hello 下列範例中，您可以設定規則*100* （優先順序高於 200 及以上） tooallow hello 遠端子網路*10.0.0.0/8*存取 toohello 虛擬機器端點。 Hello 值取代為您自己的組態需求。 hello 名稱"SharePoint ACL config"應該取代 hello 您要 toocall 此規則的好記名稱。
   
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 100 `
            –Action permit –RemoteSubnet "10.0.0.0/8" `
            –Description "SharePoint ACL config"
3. 針對其他規則，請重複 hello cmdlet，hello 值取代為您自己的組態需求。 為確定 toochange hello 規則順序 tooreflect hello 依照您想要套用的 hello 規則 toobe。 hello 低的規則數會優先於 hello 高的數字。
   
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 200 `
            –Action permit –RemoteSubnet "157.0.0.0/8" `
            –Description "web frontend ACL config"
4. 接下來，您可以建立新的端點 (Add)，或設定現有端點 (Set) 的 hello ACL。 在此範例中，我們將加入新的虛擬機器端點呼叫 hello 與"web"並更新 hello 虛擬機器端點 ACL 設定。
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Add-AzureEndpoint –Name "web" –Protocol tcp –Localport 80 - PublicPort 80 –ACL $acl1 `
        | Update-AzureVM
5. 接著，結合 hello cmdlet，並執行 hello 指令碼。 例如，hello 結合各指令程式會看起來像這樣：
   
        $acl1 = New-AzureAclConfig
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 100 `
            –Action permit –RemoteSubnet "10.0.0.0/8" `
            –Description "Sharepoint ACL config"
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 200 `
            –Action permit –RemoteSubnet "157.0.0.0/8" `
            –Description "web frontend ACL config"
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        |Add-AzureEndpoint –Name "web" –Protocol tcp –Localport 80 - PublicPort 80 –ACL $acl1 `
        |Update-AzureVM

### <a name="remove-a-network-acl-rule-that-permits-access-from-a-remote-subnet"></a>設定網路 ACL 規則以允許從遠端子網路進行存取
hello 下列範例所示方式 tooremove 網路 ACL 規則。  tooremove 的網路 ACL 規則，以允許規則對遠端子網路中，開啟 Azure PowerShell ISE。 複製和貼上 hello 下方，使用您自己的值，設定 hello 指令碼的指令碼，然後執行 hello 指令碼。

1. 第一個步驟是針對 hello 虛擬機器端點 tooget hello 網路 ACL 物件。 然後，您要移除 hello ACL 規則。 在此案例中，我們依據規則 ID 進行移除。 這只會移除 hello 規則 ID 0 從 hello ACL。 它不會移除 hello ACL 物件 hello 虛擬機器端點。
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Get-AzureAclConfig –EndpointName "web" `
        | Set-AzureAclConfig –RemoveRule –ID 0 –ACL $acl1
2. 接下來，您必須套用 hello 網路 ACL 物件 toohello 虛擬機器端點，並且更新 hello 虛擬機器。
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Set-AzureEndpoint –ACL $acl1 –Name "web" `
        | Update-AzureVM

### <a name="remove-a-network-acl-from-a-virtual-machine-endpoint"></a>從虛擬機器端點移除網路 ACL
在某些情況下，您可能想 tooremove 從虛擬機器端點的網路 ACL 物件。 toodo，開啟 Azure PowerShell ISE。 複製和貼上 hello 下方，使用您自己的值，設定 hello 指令碼的指令碼，然後執行 hello 指令碼。

        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Remove-AzureAclConfig –EndpointName "web" `
        | Update-AzureVM

## <a name="next-steps"></a>後續步驟
[什麼是網路存取控制清單 (ACL)？](virtual-networks-acl.md)

