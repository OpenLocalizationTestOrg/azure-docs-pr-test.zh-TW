---
title: "Azure 雲端服務角色常見問題集 | Microsoft Docs"
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
ms.openlocfilehash: d887f3b31693c414254dc01dac4dbdd6d9224b6d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="cloud-services-faq"></a>雲端服務常見問題集
本文提供 Microsoft Azure 雲端服務的一些常見問題解答。 您也可以造訪 [Azure 支援常見問題集](http://go.microsoft.com/fwlink/?LinkID=185083) ，以取得一般的 Azure 價格和支援資訊。 您也可以參閱 [雲端服務 VM 大小頁面](cloud-services-sizes-specs.md) 以取得大小資訊。

## <a name="certificates"></a>憑證
### <a name="where-should-i-install-my-certificate"></a>我應該將憑證安裝在何處？
* **My**  
  具有私密金鑰的應用程式憑證 (\*.pfx、\*.p12)。
* **CA**  
  所有中繼憑證都會放入此存放區 (原則和子 CA)。
* **ROOT**  
  根 CA 存放區，因此主要的根 CA 憑證應該放在這裡。

### <a name="i-cant-remove-expired-certificate"></a>無法移除過期的憑證
Azure 會防止您移除使用中的憑證。 您必須刪除使用憑證的部署，或使用不同憑證或更新的憑證來更新部署。

### <a name="delete-an-expired-certificate"></a>刪除過期的憑證
只要憑證不在使用中，您就可以使用 [Remove-AzureCertificate](https://msdn.microsoft.com/library/azure/mt589145.aspx) PowerShell Cmdlet 來移除憑證。

### <a name="i-have-expired-certificates-named-windows-azure-service-management-for-extensions"></a>我有名為 Windows Azure Service Management for Extensions 的已過期憑證
每當有擴充功能新增至雲端服務 (例如遠端桌面擴充功能)，就會建立這些憑證。 這些憑證只會用於加密和解密擴充功能的私用組態。 這些憑證是否過期並不重要。 系統不會檢查到期日期。

### <a name="certificates-i-have-deleted-keep-reappearing"></a>我已刪除的憑證一直重複出現
這些憑證會一直重複出現很可能是因為您所使用的工具，例如 Visual Studio。 每當您以使用某憑證的工具重新連線，該憑證就會再次上傳至 Azure。

### <a name="my-certificates-keep-disappearing"></a>我的憑證一直消失
當虛擬機器執行個體回收時，所有本機變更都會遺失。 請在每次角色啟動時使用 [啟動工作](cloud-services-startup-tasks.md) 將憑證安裝到虛擬機器。

### <a name="i-cannot-find-my-management-certificates-in-the-portal"></a>我在入口網站中找不到我的管理憑證
[管理憑證](../azure-api-management-certs.md)只能在 Azure 傳統入口網站中取得。 目前的 Azure 入口網站沒有使用管理憑證。 

### <a name="how-can-i-disable-a-management-certificate"></a>如何停用管理憑證？
[管理憑證](../azure-api-management-certs.md) 無法停用。 當您不想再使用它們之後，可以透過 Azure 傳統入口網站將它們刪除。

### <a name="how-do-i-create-an-ssl-certificate-for-a-specific-ip-address"></a>如何為特定 IP 位址建立 SSL 憑證？
請遵照 [建立憑證教學課程](cloud-services-certs-create.md)中的指示執行。 使用 IP 位址做為 DNS 名稱。

## <a name="security"></a>安全性
### <a name="disable-ssl-30"></a>停用 SSL 3.0
若要停用 SSL 3.0 並使用 TLS 安全性，請建立啟動工作，而其記載於此部落格文章：https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/

### <a name="add-nosniff-to-your-website"></a>將 **nosniff** 加入您的網站
若要防止用戶端探查 MIME 類型，請在您的 *web.config* 檔案中加入一項設定。

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

您也可以在 IIS 中將此加入為設定。 請參考[常見的啟動工作](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe)一文來使用下列命令。

```cmd
%windir%\system32\inetsrv\appcmd set config /section:httpProtocol /+customHeaders.[name='X-Content-Type-Options',value='nosniff']
```

### <a name="customize-iis-for-a-web-role"></a>針對 Web 角色自訂 IIS
請從[常見的啟動工作](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe)一文使用 IIS 啟動指令碼。

## <a name="scaling"></a>調整大小
### <a name="i-cannot-scale-beyond-x-instances"></a>我不能調整超過 X 個執行個體
您的 Azure 訂用帳戶對於您可以使用的核心數目有限制。 如果您已使用所有可用的核心，調整將無法運作。 例如，如果您有 100 個核心的限制，這表示您的雲端服務可以有 100 個 A1 大小的虛擬機器執行個體，或 50 個 A2 大小的虛擬機器執行個體。

## <a name="networking"></a>網路
### <a name="i-cant-reserve-an-ip-in-a-multi-vip-cloud-service"></a>無法在多 VIP 的雲端服務中保留 IP
首先，請確定您想要保留其 IP 的虛擬機器執行個體已開啟。 其次，請確定您會將保留的 IP 同時用於預備與生產部署。 **勿** 於部署正在升級時變更設定。

## <a name="remote-desktop"></a>遠端桌面
### <a name="how-do-i-remote-desktop-when-i-have-an-nsg"></a>當我有 NSG 時，應如何設定遠端桌面？
將規則加入到 NSG，以允許連接埠 **3389** 和 **20000** 上的流量。  遠端桌面使用者連接埠 **3389**。  系統已為雲端服務執行個體進行負載平衡，因此您無法直接控制要連線的執行個體。  *RemoteForwarder* 與 *RemoteAccess* 代理程式會管理 RDP 流量，並允許用戶端傳送 RDP Cookie 並指定要連線的個別執行個體。  *RemoteForwarder* 與 *RemoteAccess* 代理程式要求您必須開啟連接埠 **20000***，這在您使用 NSG 的情況下可能是封鎖的。
