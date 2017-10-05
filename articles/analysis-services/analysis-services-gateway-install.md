---
title: "安裝內部部署資料閘道 | Microsoft Docs"
description: "了解如何安裝及設定內部部署資料閘道。"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/22/2017
ms.author: owend
ms.openlocfilehash: 6ef296fb98478be9240f0231c8ad39cd2a0af995
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="install-and-configure-an-on-premises-data-gateway"></a>安裝及設定內部部署資料閘道
如果相同區域中有一或多部 Analysis Services 伺服器連線到內部部署資料來源，則需要一個內部部署閘道。 若要深入了解閘道，請參閱[內部部署資料閘道](analysis-services-gateway.md)。

## <a name="prerequisites"></a>必要條件
**最低需求：**

* .NET 4.5 Framework
* 64 位元版本的 Windows 7 / Windows Server 2008 R2 (或更新版本)

**建議配備：**

* 8 核心 CPU
* 8 GB 記憶體
* 64 位元版本的 Windows 2012 R2 (或更新版本)

**重要考量︰**

* 在設定期間，向 Azure 註冊您的閘道時，系統會選取您訂用帳戶的預設區域。 您可以選擇不同的區域。 如果您有伺服器位於多個區域中，您必須針對每個區域安裝一個閘道。 
* 閘道無法安裝在網域控制站上。
* 一部電腦只能安裝一個閘道。
* 請在電源維持開啟且不會進入睡眠狀態的電腦上安裝閘道。
* 請勿將閘道安裝於採用無線網路的電腦上。 效能會因此降低。


## <a name="download"></a>下載
 [下載閘道](https://aka.ms/azureasgateway)

## <a name="install"></a>安裝

1. 執行安裝程式。

2. 選取位置，接受條款，然後按一下 [安裝]。

   ![安裝位置和授權條款](media/analysis-services-gateway-install/aas-gateway-installer-accept.png)

3. 選取 [內部部署資料閘道 ()]。 Azure Analysis Services 不支援個人模式。

   ![選擇閘道的類型](media/analysis-services-gateway-install/aas-gateway-installer-shared.png)

4. 輸入用來登入 Azure 的帳戶。 此帳戶必須位於租用戶的 Azure Active Directory 中。 此帳戶用於閘道管理員。 

   ![輸入用來登入 Azure 的帳戶](media/analysis-services-gateway-install/aas-gateway-installer-account.png)

   > [!NOTE]
   > 如果您使用網域帳戶進行登入，該帳戶將會對應到 Azure AD 中您的組織帳戶。 您的組織帳戶將作為閘道管理員使用。

## <a name="register"></a>註冊
若要在 Azure 中建立閘道資源，您必須向閘道雲端服務註冊您安裝的本機執行個體。 

1.  選取 [在這部電腦上註冊新的閘道]。

    ![註冊](media/analysis-services-gateway-install/aas-gateway-register-new.png)

2. 輸入您的閘道名稱和復原金鑰。 根據預設，閘道會使用您訂用帳戶的預設區域。 如果您需要選取不同的區域，請選取 [變更區域]。

   ![註冊](media/analysis-services-gateway-install/aas-gateway-register-name.png)


## <a name="create-resource"></a>建立 Azure 閘道資源
在您安裝並註冊閘道之後，您需要在您的 Azure 訂用帳戶中建立閘道資源。 使用您用於註冊閘道的相同帳戶登入 Azure。

1. 在 Azure 入口網站中，按一下 [建立新服務] > [企業整合] > [內部部署資料閘道] > [建立]。

   ![建立閘道資源](media/analysis-services-gateway-install/aas-gateway-new-azure-resource.png)

2. 在 [建立連線閘道] 中，輸入下列設定：

    * **名稱**：輸入閘道資源的名稱。 

    * **訂用帳戶**︰選取要與閘道資源關聯的 Azure 訂用帳戶。 
    此訂用帳戶應該是您的伺服器所在的相同訂用帳戶。
   
      預設的訂用帳戶會由您用來登入的 Azure 帳戶來決定。

    * **資源群組**：建立資源群組，或選取現有的資源群組。

    * **位置**：選取您註冊閘道的區域。

    * **安裝名稱**︰如果您的閘道安裝還不是選取狀態，請選取已註冊的閘道。 

    完成之後，請按一下 [建立] 。

## <a name="connect-servers"></a>將伺服器連線到閘道資源

1. 在 Azure Analysis Services 伺服器概觀中，按一下 [內部部署資料閘道]。

   ![將伺服器連線至閘道](media/analysis-services-gateway-install/aas-gateway-connect-server.png)

2. 在 [挑選要連線的內部部署資料閘道] 中，選取您的閘道資源，然後按一下 [連線選取的閘道]。

   ![將伺服器連線至閘道資源](media/analysis-services-gateway-install/aas-gateway-connect-resource.png)

    > [!NOTE]
    > 如果您的閘道並未出現在清單中，您的伺服器可能不在註冊閘道時所指定的相同區域中。 

就這麼簡單。 如果您需要開啟連接埠，或進行疑難排解，請務必簽出[內部部署資料閘道](analysis-services-gateway.md)。

## <a name="next-steps"></a>後續步驟
* [ Analysis Services](analysis-services-manage.md)   
* [從 Azure Analysis Services 取得資料](analysis-services-connect.md)
