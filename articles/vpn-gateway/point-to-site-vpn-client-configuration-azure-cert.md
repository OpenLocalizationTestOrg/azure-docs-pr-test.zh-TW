---
title: "建立和安裝適用於 Azure 憑證驗證的 P2S VPN 用戶端組態檔：PowerShell：Azure | Microsoft Docs"
description: "本文可協助您對使用憑證驗證的點對站連線建立和安裝 VPN 用戶端組態檔。"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/27/2017
ms.author: cherylmc
ms.openlocfilehash: 7fe8d5e473e2c8281b1d6c8d7d5423294c428678
ms.sourcegitcommit: 3e3a5e01a5629e017de2289a6abebbb798cec736
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/27/2017
---
# <a name="create-and-install-vpn-client-configuration-files-for-native-azure-certificate-authentication-p2s-configurations"></a>建立和安裝適用於原生 Azure 憑證驗證 P2S 組態的 VPN 用戶端組態檔

VPN 用戶端組態檔包含在 ZIP 檔案內。 這些組態檔會提供原生 Windows 或 Mac IKEv2 VPN 用戶端所需的設定，以供其透過使用原生 Azure 憑證驗證的點對站連線來連線至 VNet。

>[!NOTE]
>適用於 P2S 的 IKEv2 目前為預覽版。
>

### <a name="workflow"></a>P2S 工作流程

  1. 設定 P2S 連線的 Azure VPN 閘道。
  2. 產生根憑證和用戶端憑證。 將根憑證公開金鑰上傳至 Azure，並將用戶端憑證安裝在用戶端裝置上。 系統會使用憑證來驗證要連線的使用者。
  3. 取得所選驗證選項適用的 VPN 用戶端組態，並用它來設定 Windows 和 Mac 裝置上的 VPN 用戶端。 這可讓您透過點對站連線來連線至 Azure VNet。

>[!NOTE]
>用戶端組態檔是 VNet 所使用之 VPN 組態特有的檔案。 如果您在產生 VPN 用戶端組態檔後對「點對站 VPN 組態」進行任何變更 (例如 VPN 通訊協定類型或驗證類型)，請務必為使用者裝置產生新的 VPN 用戶端組態檔。
>
>

## <a name="generate"></a>產生 VPN 用戶端組態檔

在開始之前，請確定所有要連線的使用者都已在使用者裝置上安裝有效的憑證。 如需如何安裝用戶端憑證的詳細資訊，請參閱[安裝用戶端憑證](point-to-site-how-to-vpn-client-install-azure-cert.md)。

您可以使用 PowerShell 或使用 Azure 入口網站來產生用戶端組態檔。 任一方法都會傳回相同的 zip 檔案。 將該檔案解壓縮以檢視下列資料夾：

  * **WindowsAmd64** 和 **WindowsX86**，這兩個資料夾分別包含 Windows 32 位元和 64 位元的安裝程式套件。 **WindowsAmd64** 安裝程式套件不只適用於 AMD，也適用於所有受支援的 64 位元 Windows 用戶端。
  * **Generic**，這個資料夾包含用來建立自有 VPN 用戶端組態的一般資訊。 請略過此資料夾。 當閘道上設定了 IKEv2 或 SSTP+IKEv2 時才會提供 Generic 資料夾。 如果只設定了 SSTP，則不會提供 Generic 資料夾。

### <a name="zipportal"></a>使用 Azure 入口網站產生檔案

1. 在 Azure 入口網站中，瀏覽至您想要連線之虛擬網路的虛擬網路閘道。
2. 在虛擬網路閘道頁面上，按一下 [點對站組態]。
3. 在 [點對站台組態] 頁面頂端，按一下 [下載 VPN 用戶端]。 產生用戶端組態套件需耗費幾分鐘的時間。
4. 您的瀏覽器指出用戶端組態 zip 檔可用。 它會命名為您閘道的相同名稱。 解壓縮檔案以檢視資料夾。

### <a name="zipps"></a>使用 PowerShell 產生檔案

1. 在產生 VPN 用戶端組態檔時，「-AuthenticationMethod」的值是「EapTls」。 使用下列命令來產生 VPN 用戶端組態檔：

  ```powershell
  $profile=New-AzureRmVpnClientConfiguration -ResourceGroupName "TestRG" -Name "VNet1GW" -AuthenticationMethod "EapTls"

  $profile.VPNProfileSASUrl
  ```
2. 將 URL 複製到您的瀏覽器來下載 zip 檔案，然後解壓縮檔案以檢視資料夾。

## <a name="installwin"></a>安裝 Windows VPN 用戶端組態套件

您可以在每個 Windows 用戶端電腦上使用相同的 VPN 用戶端組態套件，但前提是版本必須符合用戶端的架構。 如需用戶端支援的作業系統清單，請參閱 [VPN 閘道常見問題集](vpn-gateway-vpn-faq.md#P2S)的＜點對站＞一節。

請使用下列步驟來設定原生 Windows VPN 用戶端的憑證驗證：

1. 選取 Windows 電腦架構所對應的 VPN 用戶端組態檔。 若是 64 位元的處理器架構，請選擇 'VpnClientSetupAmd64' 安裝程式套件。 若是 32 位元的處理器架構，請選擇 'VpnClientSetupX86' 安裝程式套件。 
2. 對套件按兩下來加以安裝。 如果您看到 SmartScreen 快顯視窗，請按一下 [更多資訊]，然後按一下 [仍要執行]。
3. 在用戶端電腦上，瀏覽至 [網路設定]，然後按一下 [VPN]。 VPN 連線會顯示其連線的虛擬網路名稱。 

## <a name="installmac"></a>Mac 上的 VPN 用戶端組態 (OSX)

Azure 不提供用於原生 Azure 憑證驗證的 mobileconfig 檔案。 您必須在將會連線到 Azure 的每部 Mac 上，手動設定原生 IKEv2 VPN 用戶端。 **Generic** 資料夾含有設定所需的所有資訊。 如果未出現下載的 Generic 資料夾，則可能是未將 IKEv2 選為通道型別。 一旦選取 IKEv2 後，重新產生 zip 檔案以擷取 Generic 資料夾。 Generic 資料夾包含下列檔案：

* **VpnSettings.xml**，此檔案包含重要的設定，例如伺服器位址和通道類型。 
* **VpnServerRoot.cer**，此檔案包含所需的根憑證，以供您在 P2S 連線設定期間驗證 Azure VPN 閘道。

使用下列步驟，在 Mac 上設定用於憑證驗證的原生 VPN 用戶端。 您必須在將會連線到 Azure 的每部 Mac 上，完成下列步驟：

1. 將 **VpnServerRoot** 根憑證匯入 Mac 中。 若要這麼做，請將該檔案複製到 Mac 上並對該檔案按兩下。  
按一下 [新增] 來進行匯入。

  ![新增憑證](./media/point-to-site-vpn-client-configuration-azure-cert/addcert.png)
  
    >[!NOTE]
    >按兩下憑證可能不會顯示 [新增] 對話方塊，但是憑證已安裝在正確的存放區。 您可以在憑證類別底下的登入金鑰鏈中檢查憑證。
  
2. 開啟 [網路喜好設定] 底下的 [網路] 對話方塊，然後按一下 [+] 建立適用於 Azure VNet P2S 連線的新 VPN 用戶端連線設定檔。

  [介面] 值是 [VPN]，[VPN 類型] 值則是 [IKEv2]。 在 [服務名稱] 欄位中指定設定檔名稱，然後按一下 [建立] 以建立 VPN 用戶端連線設定檔。

  ![網路](./media/point-to-site-vpn-client-configuration-azure-cert/network.png)
3. 從 **Generic** 資料夾的 **VpnSettings.xml** 檔案複製 **VpnServer** 標記值。 將此值貼到設定檔的 [伺服器位址] 和 [遠端識別碼] 欄位。

  ![伺服器資訊](./media/point-to-site-vpn-client-configuration-azure-cert/server.png)
4. 按一下 [驗證設定]，然後選取 [憑證]。 

  ![驗證設定](./media/point-to-site-vpn-client-configuration-azure-cert/authsettings.png)
5. 按一下 [選取...] 以選擇您要用於驗證的用戶端憑證。 電腦上應該已經安裝一個用戶端憑證 (請參閱上一節 **P2S 工作流程**中的步驟 2)。

  ![憑證](./media/point-to-site-vpn-client-configuration-azure-cert/certificate.png)
6. [選擇身分識別] 會顯示一份憑證清單供您選擇。 選取適當憑證，然後按一下 [繼續]。

  ![身分識別](./media/point-to-site-vpn-client-configuration-azure-cert/identity.png)
7. 在 [地區設定識別碼] 欄位中指定憑證名稱 (來自步驟 6)。 在此範例中，名稱是 "ikev2Client.com"。 然後，按一下 [套用] 按鈕以儲存變更。

  ![apply](./media/point-to-site-vpn-client-configuration-azure-cert/applyconnect.png)
8. 在 [網路] 對話方塊中按一下 [套用] 以儲存所有變更。 然後，按一下 [連線] 以啟動 Azure VNet 的 P2S 連線。

## <a name="next-steps"></a>後續步驟

回到本文以[完成 P2S 設定](vpn-gateway-howto-point-to-site-rm-ps.md)。
