---
title: "aaaApplication 閘道整合與 Azure 資訊安全中心 |Microsoft 文件"
description: "此頁面提供如何將應用程式閘道整合到 Azure 資訊安全中心的相關資訊。"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: 
ms.assetid: e5ea5cf9-3b41-4b85-a12c-e758bff7f3ec
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: 
ms.workload: infrastructure-services
ms.date: 06/07/2017
ms.author: gwallace
ms.openlocfilehash: 6f6ace105e84c01f525ab02938e81ce040c5c9d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-integration-between-application-gateway-and-azure-security-center"></a>應用程式閘道與 Azure 資訊安全中心整合概觀

了解如何使用應用程式閘道和資訊安全中心如何保護您的 Web 應用程式資源。 應用程式閘道 web 應用程式防火牆 (WAF) 整合[資訊安全中心](../security-center/security-center-intro.md)tooprovide 順暢檢視 tooprevent，偵測及回應 toothreats toounprotected web 應用程式，您的環境中。

## <a name="overview"></a>概觀

建議在資訊安全中心使用應用程式閘道 WAF，以保護 Web 應用程式議抵禦入侵和弱點。 啟用 web 資源，而不會受到 WAF 顯示 hello 資訊安全中心，做為高嚴重性的建議。 針對 web 應用程式防火牆的建議會出現在 hello**概觀**頁面的 **應用程式**。

![與資訊安全中心整合][1]

按一下任何 web 應用程式防火牆的建議會開啟顯示 hello hello 建議事項的詳細資料的新刀鋒視窗。

## <a name="add-a-web-application-firewall-tooan-existing-resource"></a>加入 web 應用程式防火牆 tooan 現有資源

瀏覽過**更服務** > **安全性 + 身分識別** > **資訊安全中心**在 hello**資訊安全中心-概觀**刀鋒視窗中，按一下 **應用程式**。 在 hello**資訊安全中心的應用程式**刀鋒視窗中，hello 資料表包含您的訂用帳戶中偵測到的資訊安全中心的應用程式清單。

![Web 應用程式][3]

按一下與 web 應用程式的嚴重問題，您會收到 hello**應用程式的安全性健全狀況**刀鋒視窗。 在下面的 hello 影像，hello 不由 web 應用程式防火牆保護的 web 應用程式。 

![未受保護的 Web 資源][2]

按一下**加入 web 應用程式防火牆**下**建議**tooopen hello**加入 Web 應用程式防火牆**刀鋒視窗。

如果您沒有可以使用現有的應用程式閘道，或想 toocreate 新的請按一下**新建**在 hello**建立新的 Web 應用程式防火牆**刀鋒視窗中，然後按一下**Microsoft-應用程式閘道**。 這會帶領您完成 hello 步驟 toocreate 應用程式閘道。 此時，您的 Web 應用程式已新增為受保護的資源，資訊安全中心現在會追蹤這個受到 Web 應用程式防火牆保護的資源。 這不會將它新增為後端集區的成員。

如果您有現有的應用程式閘道，您可以在 [使用現有的解決方案] 中選擇它。

![新增 Web 應用程式防火牆刀鋒視窗][4]

新增資訊安全中心透過 web 應用程式 tooan 應用程式閘道不會新增為後端集區成員的 hello 資源，這必須完成 hello 應用程式閘道資源上直接。

## <a name="add-a-resource-tooan-existing-web-application-firewall"></a>新增資源 tooan 現有 web 應用程式的防火牆

瀏覽過**更服務** > **安全性 + 身分識別** > **資訊安全中心**在 hello**資訊安全中心-概觀**刀鋒視窗中，按一下 **合作夥伴解決方案**。 現有的資訊安全中心感知應用程式閘道顯示在 hello**協力廠商解決方案**刀鋒視窗。

![合作夥伴解決方案][7]

按一下**連結應用程式**tooopen hello**連結應用程式**刀鋒視窗中，這裡有個 hello 選項 tooselect 現有應用程式。 選擇 hello 應用程式 tooprotect，然後按一下**確定**。 這不會新增 hello web 應用程式 toohello 後端集區的 hello 應用程式閘道。 讓資訊安全中心能夠追蹤它，這樣可以設定為受保護資源的 hello 資源。 tooadd hello 做為後端集區成員的資源，這必須完成 hello 應用程式閘道上，從 hello 目前刀鋒視窗，您可以按一下**方案主控台**toobe 採取 toohello 應用程式閘道資源，您可以在其中加入 hello web應用程式 toohello 後端集區。

![合作夥伴解決方案應用程式][6]

## <a name="finalize-configuration"></a>完成設定

資訊安全中心會追蹤應用程式加入 tooan 應用程式閘道做為受保護的資源。  它會監視此資源的 hello 健全狀況，並確保受應用程式閘道。 hello 下一個步驟是 tooadd hello 私人 IP、 公用 IP 或 NIC 的虛擬機器 toohello 後端集區的 hello 應用程式閘道。 這麼做的其他建議直到**完成應用程式保護**hello 資源加入之前顯示。

![新增 Web 應用程式防火牆刀鋒視窗][5]

## <a name="security-alerts"></a>安全性警示

資訊安全中心內瀏覽過**偵測** > **安全性警示**。  在這裡可以找到您的應用程式閘道的 WAF 警示。 警示是依 WAF 規則細分。

![安全性警示][8]

按一下規則會提供該特定 WAF 規則的警示清單。 每個警示會顯示有關 hello 尋找其他詳細資料。 hello 詳細資料會提供連結 toohello 應用程式閘道。
 
![警示詳細資料][9]

## <a name="next-steps"></a>後續步驟

toolearn tooenable web 應用程式防火牆上現有的應用程式閘道的瀏覽[建立或更新 Azure 應用程式閘道與 web 應用程式防火牆](application-gateway-web-application-firewall-portal.md#add-web-application-firewall-to-an-existing-application-gateway)

[1]: ./media/application-gateway-integration-security-center/figure1.png
[2]: ./media/application-gateway-integration-security-center/figure2.png
[3]: ./media/application-gateway-integration-security-center/figure3.png
[4]: ./media/application-gateway-integration-security-center/figure4.png
[5]: ./media/application-gateway-integration-security-center/figure5.png
[6]: ./media/application-gateway-integration-security-center/figure6.png
[7]: ./media/application-gateway-integration-security-center/figure7.png
[8]: ./media/application-gateway-integration-security-center/securitycenter.png
[9]: ./media/application-gateway-integration-security-center/figure9.png