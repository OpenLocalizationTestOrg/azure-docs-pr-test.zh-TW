---
title: "Azure Active Directory Domain Services：管理指南 | Microsoft Docs"
description: "加入 Windows 虛擬機器 tooa 受管理的網域使用 Azure PowerShell 及 hello 傳統部署模型。"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 9143b843-7327-43c3-baab-6e24a18db25e
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 21bc5930d84c5368a120f9d81f09320e2a0168fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-windows-server-virtual-machine-tooa-managed-domain-using-powershell"></a>加入 Windows Server 虛擬機器 tooa 受管理的網域使用 PowerShell
> [!div class="op_single_selector"]
> * [Azure 傳統入口網站 - Windows](active-directory-ds-admin-guide-join-windows-vm.md)
> * [PowerShell - Windows](active-directory-ds-admin-guide-join-windows-vm-classic-powershell.md)
>
>

<br>

> [!IMPORTANT]
> Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。 本文說明如何使用 hello 傳統部署模型。 Azure AD 網域服務目前不支援 hello 資源管理員的模型。
>
>

這些步驟顯示如何 toocustomize 一組的 Azure PowerShell 命令，建立並預先設定 windows Azure 虛擬機器使用的建置組塊方法。 這些步驟可協助您建立 windows Azure 虛擬機器，並將其加入 tooan Azure AD 網域服務受管理的網域。

這些步驟遵循建立 Azure PowerShell 命令集合的填空方法。 如果您是新 tooPowerShell 或想 tooknow 哪些值 toospecify 成功的組態，這種方法十分有用。 進階的 PowerShell 使用者可以採取 hello 命令，並以取代其值為 hello 變數 （hello 行開頭為"$"）。

如果還沒有這麼做，使用中的 hello 指示[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview) tooinstall Azure PowerShell，在本機電腦上的。 然後，開啟 Windows PowerShell 命令提示字元。

## <a name="step-1-add-your-account"></a>步驟 1︰加入您的帳戶
1. 在 hello PowerShell 提示字元中輸入**Add-azureaccount**按一下**Enter**。
2. 輸入您 Azure 訂用帳戶相關聯的 hello 電子郵件地址，然後按一下**繼續**。
3. 輸入 hello 您帳戶的密碼。
4. 按一下 [ **登入**]。

## <a name="step-2-set-your-subscription-and-storage-account"></a>步驟 2：設定您的訂用帳戶和儲存體帳戶
Hello Windows PowerShell 命令提示字元中執行這些命令來設定您的 Azure 訂用帳戶和儲存體帳戶。 Hello 括在引號，包括 hello < 和 > 字元內的所有項目取代 hello 正確名稱。

    $subscr="<subscription name>"
    $staccount="<storage account name>"
    Select-AzureSubscription -SubscriptionName $subscr –Current
    Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

您可以從 hello 的 hello hello 輸出的訂用帳戶名稱屬性來取得 hello 正確的訂用帳戶名稱**Get-azuresubscription**命令。 您可以從 hello Label 屬性的 hello hello 輸出取得 hello 正確的儲存體帳戶名稱**Get AzureStorageAccount**命令之後執行 hello **Select-azuresubscription**命令。

## <a name="step-3-step-by-step-walkthrough---provision-hello-virtual-machine-and-join-it-toohello-managed-domain"></a>步驟 3： 逐步解說-佈建 hello 虛擬機器，並將其聯結 toohello 受管理的網域
以下是 hello 對應 Azure PowerShell 命令集 toocreate 之間可讀性的每個區塊的空白行與此虛擬機器。

指定 hello Windows 虛擬機器 toobe 佈建的相關資訊。

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

D、 DS 或 G 系列虛擬機器的 hello InstanceSize 值，請參閱[虛擬機器和 Azure 的雲端服務大小](https://msdn.microsoft.com/library/azure/dn197896.aspx)。

提供有關 hello 受管理的網域資訊。

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

指定 hello hello 雲端服務名稱。

    $svcname="Contoso100-test"

指定 hello VM 應加入的虛擬網路 toowhich hello hello 名稱。 確定此虛擬網路中有該 hello AAD DS 受管理網域。

    $vnetname="MyPreviewVnet"

選取 VM 映像使用 toobe tooprovision hello VM hello。

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

設定 hello VM-組 VM 名稱，使用的執行個體大小及影像 toobe。

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

取得 hello VM 的本機系統管理員認證。 選擇本機系統管理員的強式密碼。

    $localadmincred=Get-Credential –Message "Type hello name and password of hello local administrator account."

取得屬於 too'AAD DC Administrators' 群組 toojoin VM toohello 受管理的網域使用者帳戶的認證。 請勿指定 hello 網域名稱-的執行個體，在本例中，我們在此指定 'bob' hello 使用者名稱。

    $domainadmincred=Get-Credential –Message "Now type hello name (DO NOT INCLUDE hello DOMAIN) and password of an account in hello AAD DC Administrators group, that has permission tooadd hello machine toohello domain."

設定 hello VM-指定網域聯結需求 （& s） 所需的認證。

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

設定 hello VM 子網路。

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

選擇性： 點 toohello 的 hello 網域的 IP 位址。 如果您設定 hello IP 位址的 hello Azure AD 網域服務受管理的網域 toobe hello hello 虛擬網路的 DNS 伺服器，就不需要此步驟。

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

現在，佈建 hello 已加入網域的 Windows VM。

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="script-tooprovision-a-windows-vm-and-automatically-join-it-tooan-aad-domain-services-managed-domain"></a>指令碼 tooprovision Windows VM，並自動將其加入 tooan AAD 網域服務受管理的網域
這個 PowerShell 命令集建立企業營運伺服器的虛擬機器：

* 使用 hello Windows Server 2012 R2 Datacenter 映像。
* 是超小的虛擬機器。
* 具有 hello Contoso100 測試的名稱。
* 會自動網域聯結的 toohello contoso100 受管理的網域。
* 加入 toohello hello 與相同虛擬網路管理網域。

以下是 hello 完整的範例指令碼 toocreate hello Windows 虛擬機器，並自動將其加入 toohello Azure AD 網域服務受管理的網域。

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

    $svcname="Contoso100-test"
    $vnetname="MyPreviewVnet"

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $localadmincred=Get-Credential –Message "Type hello name and password of hello local administrator account."

    $domainadmincred=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account in hello AAD DC Administrators group, that has permission tooadd hello machine toohello domain."

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="related-content"></a>相關內容
* [Azure AD Domain Services - 入門指南](active-directory-ds-getting-started.md)
* [Administer an Azure AD Domain Services managed domain (管理 Azure AD 網域服務受管理的網域)](active-directory-ds-admin-guide-administer-domain.md)
