---
title: "aaaAzure 執行個體層級 （傳統） 的公用 IP 位址 |Microsoft 文件"
description: "了解執行個體層級公用 IP (ILPIP) 位址及如何 toomanage 它們使用 PowerShell。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 07eef6ec-7dfe-4c4d-a2c2-be0abfb48ec5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2016
ms.author: jdial
ms.openlocfilehash: 832143ee6fdd80b634e1cebfddc759a8cacda583
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="instance-level-public-ip-classic-overview"></a>執行個體層級公用 IP (Classic) 概觀
執行個體層級公用 IP (ILPIP) 是您在 tooa VM 或雲端服務角色執行個體，而不是 VM 或角色執行個體位於 toohello 雲端服務可以直接指派的公用 IP 位址。 ILPIP 不接受 hello 取代 hello 虛擬 IP (VIP) 指派 tooyour 雲端服務。 而是其他 IP 位址，您可以使用 tooconnect 直接 tooyour VM 或角色執行個體。

> [!IMPORTANT]
> Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json)。 本文說明如何使用 hello 傳統部署模型。 Microsoft 建議您透過 Resource Manager 建立 VM。 請確定您了解 [IP 位址](virtual-network-ip-addresses-overview-classic.md) 在 Azure 中的運作方式。

![ILPIP 和 VIP 之間的差異](./media/virtual-networks-instance-level-public-ip/Figure1.png)

圖 1 所示，使用 VIP 存取 hello 雲端服務、 hello 時個別 Vm 通常會使用存取 VIP:&lt;連接埠號碼&gt;。 藉由指派 ILPIP tooa 特定 VM，VM 可以存取直接使用該 IP 位址。

當您在 Azure 中建立雲端服務時，對應的 DNS A 記錄會自動建立 tooallow 存取 toohello 服務透過完整的網域名稱 (FQDN)，而不是使用 hello 實際 VIP。 相同的程序會針對 ILPIP，讓存取 toohello VM 或角色執行個體的 FQDN 而不是 hello ILPIP hello。 比方說，如果您建立名為雲端服務*contosoadservice*，並設定名為 web 角色*contosoweb*與兩個執行個體，Azure 的暫存器 hello 遵循 A 記錄 hello 執行個體：

* contosoweb\_IN_0.contosoadservice.cloudapp.net
* contosoweb\_IN_1.contosoadservice.cloudapp.net 

> [!NOTE]
> 您只能針對每個 VM 或角色執行個體指派一個 ILPIP。 您可以使用向上 too5 ILPIPs 每個訂閱。 ILPIP 不支援多個 NIC VM。
> 
> 

## <a name="why-would-i-request-an-ilpip"></a>為什麼我要要求 ILPIP？
如果您想要 toobe 無法 tooconnect tooyour VM 或角色執行個體使用 IP 位址直接指派 tooit，而不是使用 hello 雲端服務 VIP:&lt;連接埠號碼&gt;，要求 ILPIP VM 或角色執行個體。

* **作用中 FTP** -指派 ILPIP tooa VM 後，它可以接收任何連接埠的流量。 端點不需要 hello VM tooreceive 流量。  如需 hello FTP 通訊協定的詳細資訊，請參閱 (https://en.wikipedia.org/wiki/File_Transfer_Protocol#Protocol_overview) [FTP 通訊協定概觀]。
* **輸出 IP** -源自的 hello VM 是輸出流量對應 toohello ILPIP 為 hello 來源和 hello ILPIP 唯一識別 hello VM tooexternal 實體。

> [!NOTE]
> 在過去 hello ILPIP 位址會是參照的 tooas 公用 IP (PIP) 位址。
> 

## <a name="manage-an-ilpip-for-a-vm"></a>管理 VM 的 ILPIP
toocreate、 指派及移除的 Vm 所傳來的 ILPIPs hello 下列工作可讓您：

### <a name="how-toorequest-an-ilpip-during-vm-creation-using-powershell"></a>如何 toorequest ILPIP 期間使用 PowerShell 建立的 VM
hello 下列 PowerShell 指令碼會建立名為雲端服務*FTPService*，從 Azure 擷取映像，建立名為 VM *FTPInstance*使用 hello 擷取映像、 設定 hello VM toouse ILPIP，並將 hello VM toohello 新服務：

```powershell
New-AzureService -ServiceName FTPService -Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"} `
New-AzureVMConfig -Name FTPInstance -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| Set-AzurePublicIP -PublicIPName ftpip | New-AzureVM -ServiceName FTPService -Location "Central US"
```

### <a name="how-tooretrieve-ilpip-information-for-a-vm"></a>如何為 vm tooretrieve ILPIP 資訊
執行下列 PowerShell 命令的 hello tooview hello hello 與 hello 至上一個指令碼，在建立 VM 的 ILPIP 資訊，並觀察 hello 值*PublicIPAddress*和*PublicIPName*:

```powershell
Get-AzureVM -Name FTPInstance -ServiceName FTPService
```

預期的輸出：
 
    DeploymentName              : FTPService
    Name                        : FTPInstance
    Label                       : 
    VM                          : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.PersistentVM
    InstanceStatus              : ReadyRole
    IpAddress                   : 100.74.118.91
    InstanceStateDetails        : 
    PowerState                  : Started
    InstanceErrorCode           : 
    InstanceFaultDomain         : 0
    InstanceName                : FTPInstance
    InstanceUpgradeDomain       : 0
    InstanceSize                : Small
    HostName                    : FTPInstance
    AvailabilitySetName         : 
    DNSName                     : http://ftpservice888.cloudapp.net/
    Status                      : ReadyRole
    GuestAgentStatus            :   Microsoft.WindowsAzure.Commands.ServiceManagement.Model.GuestAgentStatus
    ResourceExtensionStatusList : {Microsoft.Compute.BGInfo}
    PublicIPAddress             : 104.43.142.188
    PublicIPName                : ftpip
    NetworkInterfaces           : {}
    ServiceName                 : FTPService
    OperationDescription        : Get-AzureVM
    OperationId                 : 568d88d2be7c98f4bbb875e4d823718e
    OperationStatus             : OK

### <a name="how-tooremove-an-ilpip-from-a-vm"></a>如何從 VM ILPIP tooremove
tooremove hello ILPIP 加入 hello 至上一個指令碼，執行下列 PowerShell 命令的 hello toohello VM:

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Remove-AzurePublicIP | Update-AzureVM
```

### <a name="how-tooadd-an-ilpip-tooan-existing-vm"></a>如何 tooadd ILPIP tooan 現有的 VM
tooadd ILPIP toohello VM 建立使用 hello 指令碼之前，執行下列命令的 hello:

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Set-AzurePublicIP -PublicIPName ftpip2 | Update-AzureVM
```

## <a name="manage-an-ilpip-for-a-cloud-services-role-instance"></a>管理雲端服務角色執行個體的 ILPIP

tooadd ILPIP tooa 雲端服務角色執行個體，完成下列步驟的 hello:

1. 下載 hello.cscfg 檔案中 hello 步驟 hello 雲端服務，藉由完成 hello [tooConfigure 雲端服務如何](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg)發行項。
2. 更新 hello.cscfg 檔案加 hello`InstanceAddress`項目。 hello 下列範例會加入名為 ILPIP *MyPublicIP* tooa 角色執行個體名為*WebRole1*: 

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <ServiceConfiguration serviceName="ILPIPSample" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="4" osVersion="*" schemaVersion="2014-01.2.3">
      <Role name="WebRole1">
        <Instances count="1" />
          <ConfigurationSettings>
        <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
          </ConfigurationSettings>
      </Role>
      <NetworkConfiguration>
        <AddressAssignments>
          <InstanceAddress roleName="WebRole1">
        <PublicIPs>
          <PublicIP name="MyPublicIP" domainNameLabel="MyPublicIP" />
            </PublicIPs>
          </InstanceAddress>
        </AddressAssignments>
      </NetworkConfiguration>
    </ServiceConfiguration>
    ```
3. 上傳 hello.cscfg 檔案中 hello 步驟 hello 雲端服務，藉由完成 hello [tooConfigure 雲端服務如何](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg)發行項。

## <a name="next-steps"></a>後續步驟
* 了解如何[IP 定址](virtual-network-ip-addresses-overview-classic.md)hello 傳統部署模型中的運作方式。
* 深入了解 [保留的 IP](virtual-networks-reserved-public-ip.md)。
