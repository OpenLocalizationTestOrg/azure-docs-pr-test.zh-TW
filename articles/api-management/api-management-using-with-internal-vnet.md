---
title: "aaaHow toouse Azure API 管理與內部虛擬網路 |Microsoft 文件"
description: "深入了解如何 toosetup 和內部虛擬網路中設定 Azure API 管理。"
services: api-management
documentationcenter: 
author: solankisamir
manager: kjoshi
editor: 
ms.assetid: dac28ccf-2550-45a5-89cf-192d87369bc3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 8d25de14e0c0bebe7ba7b47ca432ea4e45dde312
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-api-management-service-with-internal-virtual-network"></a>搭配使用 Azure API 管理服務與內部虛擬網路
API 管理可以使用 Azure 虛擬網路 (Vnet)，來管理應用程式開發介面無法存取 hello 網際網路上。 有多種 VPN 技術可提供 toomake hello 連線和 API 管理可被部署在 hello VNET 內的兩個主要模式：
* 外部
* 內部

## <a name="overview"> </a>概觀
API 管理中的內部虛擬網路模式部署時，所有 hello 服務端點 （閘道、 開發人員入口網站、 發行者入口網站中，直接管理和 Git），才都會顯示虛擬網路內部的控制存取權。 無 hello 服務端點登錄在 hello 公用 DNS 伺服器上。

使用 API 管理內部的模式中，您可以達到下列案例的 hello
* 協力廠商可在您的私人資料中心外使用站對站或 ExpressRoute VPN 連線存取資料中心時，可以安全地將 API 裝載在您的私人資料中心。
* 透過通用閘道器公開您的雲端型 API 和內部部署 API，藉此實現混合式雲端案例。
* 使用單一閘道器端點，管理裝載在多個地理位置的 API。 

## <a name="enable-vpn"> </a>在內部虛擬網路中建立 API 管理
hello 內部虛擬網路中的 API 管理服務是內部的負載 Balancer(ILB) 後面進行裝載。 hello hello ILB 的 IP 位址位於 hello [RFC1918](http://www.faqs.org/rfcs/rfc1918.html)範圍。  

### <a name="enable-vnet-connection-using-azure-portal"></a>使用 Azure 入口網站啟用 VNET 連線
第一次使用 hello 步驟建立 hello API 管理服務[建立 API 管理服務][Create API Management service]。 然後設定 API 管理 toobe 部署在虛擬網路內。

![在內部虛擬網路中設定 APIM 的功能表][api-management-using-internal-vnet-menu]

Hello 部署成功之後，您應該在 hello 儀表板上看到 hello 內部的虛擬 IP 位址，您的服務。

![已設定內部 VNET 的 API 管理儀表板][api-management-internal-vnet-dashboard]

### <a name="enable-vnet-connection-using-powershell-cmdlets"></a>使用 PowerShell Cmdlet 啟用 VNET 連線
您也可以啟用 VNET 連線使用 hello PowerShell cmdlet。

* **建立 API 管理服務內 VNET**： 使用 hello cmdlet[新增 AzureRmApiManagement](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) toocreate Azure API 管理服務內的 VNET，並設定它 toouse hello 內部 VNET 類型。

* **部署在 VNET 內現有的 API 管理服務**： 使用 hello cmdlet[更新 AzureRmApiManagementDeployment](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) toomove 現有的 Azure API 管理服務的虛擬網路內，並設定它 toouse內部 VNET 型別。

## <a name="apim-dns-configuration"></a> DNS 設定
使用外部虛擬網路模式的 API 管理時，DNS 是由 Azure 管理。 內部虛擬網路模式，您必須 toomanage 自己的 DNS。

> [!NOTE]
> API 管理服務不會接聽 toorequests 即將於 IP 位址。 它只會回應 toorequests toohello 的服務端點上設定主機名稱 （其中包括閘道、 開發人員入口網站、 發行者入口網站中，直接管理端點和 git）。

### <a name="access-on-default-host-names"></a>預設主機名稱上的存取︰
當您建立 API 管理服務在公用 Azure 雲端中，例如名為"contoso"時，hello 下列服務端點是預設設定。

>   閘道 / 代理程式 - contoso.azure-api.net

> 發行者入口網站和開發人員入口網站 - contoso.portal.azure-api.net

> 直接管理端點 - contoso.management.azure-api.net

>   Git - contoso.scm.azure-api.net

tooaccess 這些 API 管理服務端點，您可以在其中部署應用程式開發介面管理連線的子網路 toohello 虛擬網路中建立虛擬機器。 假設您的服務的 hello 內部的虛擬 IP 位址 10.0.0.5，您可以執行 hello 主機檔案對應 （%systemdrive%\drivers\etc\hosts)，如下所示：

> 10.0.0.5    contoso.azure-api.net

> 10.0.0.5    contoso.portal.azure-api.net

> 10.0.0.5    contoso.management.azure-api.net

> 10.0.0.5    contoso.scm.azure-api.net

然後，您就可以存取所有 hello 服務端點從 hello 您建立虛擬機器。 如果在虛擬網路中使用自訂 DNS 伺服器，您也可以建立 A DNS 記錄，並從虛擬網路中的任何地方存取這些端點。 

### <a name="access-on-custom-domain-names"></a>自訂網域名稱上的存取：
如果您不想 tooaccess hello 與 hello 預設主控件名稱的 API 管理服務，您可以設定所有服務端點類似如下的自訂網域名稱

![設定 API 管理的自訂網域][api-management-custom-domain-name]

然後您可以建立 A 記錄，DNS 伺服器 tooaccess 中也就是只從您的虛擬網路中存取這些端點。

## <a name="related-content"> </a>相關內容
* [在 VNET 中設定 APIM 常見的網路組態問題][Common Network Configuration Issues]
* [虛擬網路常見問題集](../virtual-network/virtual-networks-faq.md)
* [在 DNS 中建立 A 記錄](https://msdn.microsoft.com/en-us/library/bb727018.aspx)

[api-management-using-internal-vnet-menu]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-menu.png
[api-management-internal-vnet-dashboard]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-dashboard.png
[api-management-custom-domain-name]: ./media/api-management-using-with-internal-vnet/api-management-custom-domain-name.png

[Create API Management service]: api-management-get-started.md#create-service-instance
[Common Network Configuration Issues]: api-management-using-with-vnet.md#network-configuration-issues
