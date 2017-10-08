---
title: "aaaAzure 雲端服務角色常見問題集 |Microsoft 文件"
description: "關於 Azure 雲端服務的常見問題集。 關於憑證、Web 角色和背景工作角色的一些常見問題解答。"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: b07a1990e031e60ae919a5f7c636945b89c7d3a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-services-faq"></a>雲端服務常見問題集
本文提供 Microsoft Azure 雲端服務的一些常見問題解答。 您也可以造訪 hello [Azure 支援常見問題集](http://go.microsoft.com/fwlink/?LinkID=185083)一般 Azure 定價和支援資訊。 此外，您也可以參考 hello[雲端服務 VM 大小頁面](cloud-services-sizes-specs.md)大小資訊。

## <a name="certificates"></a>憑證
### <a name="where-should-i-install-my-certificate"></a>我應該將憑證安裝在何處？
* **My**  
  具有私密金鑰的應用程式憑證 (\*.pfx、\*.p12)。
* **CA**  
  所有中繼憑證都會放入此存放區 (原則和子 CA)。
* **ROOT**  
  hello 根 CA 存放區，讓您的主要根 CA 憑證應該在這裡。

### <a name="i-cant-remove-expired-certificate"></a>無法移除過期的憑證
Azure 會防止您移除使用中的憑證。 您需要使用 hello 憑證 tooeither 刪除 hello 部署或更新 hello 部署具有不同或更新憑證。

### <a name="delete-an-expired-certificate"></a>刪除過期的憑證
只要 hello 憑證不在使用中，您可以使用 hello[移除 AzureCertificate](https://msdn.microsoft.com/library/azure/mt589145.aspx) PowerShell cmdlet tooremove 憑證。

### <a name="i-have-expired-certificates-named-windows-azure-service-management-for-extensions"></a>我有名為 Windows Azure Service Management for Extensions 的已過期憑證
擴充功能加入 toohello 雲端服務，例如 hello 遠端桌面延伸模組時，會建立這些憑證。 這些憑證只用於加密和解密 hello 擴充的 hello 私用組態。 這些憑證是否過期並不重要。 不會檢查 hello 到期日。

### <a name="certificates-i-have-deleted-keep-reappearing"></a>我已刪除的憑證一直重複出現
這些憑證會一直重複出現很可能是因為您所使用的工具，例如 Visual Studio。 每當您重新連線使用的憑證的工具，將重新予以上傳的 tooAzure。

### <a name="my-certificates-keep-disappearing"></a>我的憑證一直消失
當 hello 虛擬機器執行個體回收時，所有本機變更都會遺失。 使用[啟動工作](cloud-services-startup-tasks.md)tooinstall 憑證 toohello 虛擬機器的每個時間 hello 角色啟動。

### <a name="i-cannot-find-my-management-certificates-in-hello-portal"></a>我找不到我的管理憑證在 hello 入口網站
[管理憑證](../azure-api-management-certs.md)hello Azure 傳統入口網站中才有。 hello 目前的 Azure 入口網站並不會使用管理憑證。 

### <a name="how-can-i-disable-a-management-certificate"></a>如何停用管理憑證？
[管理憑證](../azure-api-management-certs.md) 無法停用。 您刪除它們透過 hello Azure 傳統入口網站時您不希望 toobe 不再使用。

### <a name="how-do-i-create-an-ssl-certificate-for-a-specific-ip-address"></a>如何為特定 IP 位址建立 SSL 憑證？
依照指示進行 hello hello[建立憑證的教學課程](cloud-services-certs-create.md)。 Hello DNS 名稱作為 hello IP 位址。

## <a name="security"></a>安全性
### <a name="disable-ssl-30"></a>停用 SSL 3.0
toodisable SSL 3.0 和使用 TLS 安全性，建立啟動工作，而其已記錄在此部落格文章： https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/

### <a name="add-nosniff-tooyour-website"></a>新增**nosniff** tooyour 網站
tooprevent 用戶端從探測 hello MIME 類型，新增設定，在您*web.config*檔案。

```xml
<configuration>
   <system.webServer>
      <httpProtocol>
         <customHeaders>
            <add name="X-Content-Type-Options" value="nosniff" />
         </customHeaders>
      </httpProtocol>
   </system.webServer>
</configuration>
```

您也可以在 IIS 中將此加入為設定。 使用 hello 下列命令以 hello[常見的啟動工作](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe)發行項。

```cmd
%windir%\system32\inetsrv\appcmd set config /section:httpProtocol /+customHeaders.[name='X-Content-Type-Options',value='nosniff']
```

### <a name="customize-iis-for-a-web-role"></a>針對 Web 角色自訂 IIS
使用 hello IIS 啟動指令碼從 hello[常見的啟動工作](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe)發行項。

## <a name="scaling"></a>調整大小
### <a name="i-cannot-scale-beyond-x-instances"></a>我不能調整超過 X 個執行個體
您的 Azure 訂閱 hello 您可以使用的核心數目的上限。 調整將無法運作如果您已使用所有可用的 hello 核心。 例如，如果您有 100 個核心的限制，這表示您的雲端服務可以有 100 個 A1 大小的虛擬機器執行個體，或 50 個 A2 大小的虛擬機器執行個體。

## <a name="networking"></a>網路
### <a name="i-cant-reserve-an-ip-in-a-multi-vip-cloud-service"></a>無法在多 VIP 的雲端服務中保留 IP
首先，請確定您正嘗試 tooreserve hello IP 用於該 hello 虛擬機器執行個體已開啟。 第二，請確定您麻煩 hello 預備和生產環境部署使用保留 Ip。 **不這麼做**hello 部署正在升級時，變更 hello 設定。

## <a name="remote-desktop"></a>遠端桌面
### <a name="how-do-i-remote-desktop-when-i-have-an-nsg"></a>當我有 NSG 時，應如何設定遠端桌面？
新增規則 toohello 允許連接埠上的流量的 NSG **3389**和**20000**。  遠端桌面使用者連接埠 **3389**。  雲端服務執行個體是負載平衡，因此您無法直接控制至哪一個執行個體 tooconnect。  hello *RemoteForwarder*和*RemoteAccess*代理程式管理 RDP 流量，並允許 hello 用戶端 toosend RDP cookie，並指定要個別執行個體 tooconnect。  hello *RemoteForwarder*和*RemoteAccess*代理程式需要該連接埠**20000*** 開啟，如果您有 NSG 可能會封鎖連接。
