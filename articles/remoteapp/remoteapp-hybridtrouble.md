---
title: "建立 RemoteApp 的混合式集合 aaaTroubleshoot |Microsoft 文件"
description: "深入了解如何 tootroubleshoot RemoteApp 混合式集合建立失敗"
services: remoteapp
documentationcenter: 
author: vkbucha
manager: mbaldwin
ms.assetid: b32033ee-8d52-4e74-bb78-86ca873c34e2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: cc426f24bd0c349a8862d54acbafa9cf84446f4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-creating-azure-remoteapp-hybrid-collections"></a>建立 Azure RemoteApp 混合式集合疑難排解
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。
> 
> 

混合式集合中裝載，並將資料儲存在 hello Azure 雲端，但也可讓使用者存取資料和儲存在您的區域網路上的資源。 使用者可以使用與 Azure Active Directory 同步處理或同盟的公司認證進行登入，以存取應用程式。 您可以部署使用現有 Azure 虛擬網路的混合式集合，或者可以建立新的虛擬網路。 建議您建立或使用虛擬網路子網路，而其預期 Azure RemoteApp 未來成長的 CIDR 範圍夠大。

是否尚未建立集合？ 請參閱[建立混合式集合](remoteapp-create-hybrid-deployment.md)hello 的步驟。

如果您無法建立您的集合，或如果 hello 集合無法正常 hello 方式您認為它應該簽出 hello 下列資訊。

## <a name="your-image-is-invalid"></a>您的映像無效
如果您正在等候 Azure tooprovision 您的集合時，您會看到類似 「 GoldImageInvalid 」 的訊息，表示您的範本映像不符合 hello[定義映像需求](remoteapp-imagereqs.md)。 因此，請移讀取這些[需求](remoteapp-imagereqs.md)，修正您的映像，然後再試 toocreate 集合一次。

## <a name="does-your-vnet-have-network-security-groups-defined"></a>VNET 是否已定義網路安全性群組？
如果您有在您使用集合的 hello 子網路上定義的網路安全性群組，請確定這些[Url 和連接埠](remoteapp-ports.md)從您的子網路中存取。

您可以加入額外的網路安全性群組 toohello Vm 部署由您 hello 子網路都會為更嚴格的控制。

## <a name="are-you-using-your-own-dns-servers-and-are-they-accessible-from-your-vnet-subnet"></a>是否正在使用專屬 DNS 伺服器？ 是否可以從 VNET 子網路存取它們？
> [!NOTE]
> 您有 toomake 確定您的 VNET 中的 DNS 伺服器一律都已啟動的 hello 和永遠無法 tooresolve 裝載 hello VNET 中的 hello 虛擬機器。 請勿在此使用 Google DNS。
> 
> 

對於混合式集合，您使用專屬 DNS 伺服器。 您指定這些資源或透過 hello 管理入口網站中您的網路組態結構描述當您建立虛擬網路。 它們會指定容錯移轉的方式 （相對於的 tooround 循環配置資源） 中的 hello 順序會使用 DNS 伺服器。  
請參閱太[Vm 和角色執行個體的名稱解析](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md)toomake 確定您的 DNS 伺服器是設定的 correcly。

請確定您的集合的 hello DNS 伺服器可存取，而且可從您指定此集合的 hello VNET 子網路。

例如：

    <VirtualNetworkConfiguration>
    <Dns>
      <DnsServers>
        <DnsServer name="" IPAddress=""/>
      </DnsServers>
    </Dns>
    </VirtualNetworkConfiguration>

![定義 DNS](./media/remoteapp-hybridtrouble/dnsvpn.png)

## <a name="are-you-using-an-active-directory-domain-controller-in-your-collection"></a>是否在您的集合中使用 Active Directory 網域控制站？
目前只有一個 Active Directory 網域才能與 Azure RemoteApp 相關聯。 hello 混合式集合支援使用目錄同步工具，從 Windows Server Active Directory 部署; 已同步 Azure Active Directory 帳戶具體來說，或是與 hello 密碼同步處理選項進行同步處理與 Active Directory Federation Services (AD FS) 同盟設定進行同步處理。 您需要 toocreate 的自訂網域，以符合您在內部部署網域的 hello UPN 網域尾碼，並設定目錄整合。

如需詳細資訊，請參閱 [設定 Azure RemoteApp 的 Active Directory](remoteapp-ad.md) 。

請確定提供的 hello 網域詳細資料有效，然後 hello 網域控制站是從 VM 建立 hello 子網路用於 Azure 遠端應用程式中的 hello。 也請確定提供的認證有權限 tooadd 電腦 toohello 提供網域，請提供 hello AD 名稱 hello 服務帳戶可以是從 hello hello VNET 中提供的 DNS 解析。

## <a name="what-domain-name-did-you-specify-when-you-created-your-collection"></a>在您建立集合時指定哪個網域名稱？
您建立或加入 hello 網域名稱必須是內部網域名稱 （非您 Azure AD 網域名稱），而且必須可解析的 DNS 格式 (contoso.local)。 例如，您有 Active Directory 內部名稱 (contoso.local) 和 Active Directory UPN (contoso.com)-時，您有 toouse hello 內部名稱建立您的集合。

