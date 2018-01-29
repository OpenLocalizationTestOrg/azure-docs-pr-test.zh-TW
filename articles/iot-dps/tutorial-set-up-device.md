---
title: "為裝置設定 Azure IoT 中樞裝置佈建服務 | Microsoft Docs"
description: "在裝置製造過程中將裝置設定為透過 IoT 中樞裝置佈建服務進行佈建"
services: iot-dps
keywords: 
author: dsk-2015
ms.author: dkshir
ms.date: 09/05/2017
ms.topic: tutorial
ms.service: iot-dps
documentationcenter: 
manager: timlt
ms.devlang: na
ms.custom: mvc
ms.openlocfilehash: 835a54f147b9ea543df21e7dfeb226ac42aceda3
ms.sourcegitcommit: 357afe80eae48e14dffdd51224c863c898303449
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/15/2017
---
# <a name="set-up-a-device-to-provision-using-the-azure-iot-hub-device-provisioning-service"></a>將裝置設定為使用 Azure IoT 中樞裝置佈建服務進行佈建

在上一個教學課程中，您已了解如何將 Azure IoT 中樞裝置佈建服務設定為自動將裝置佈建到 IoT 中樞。 本教學課程則會指引您如何在製造過程中為裝置進行設定，以便您可以根據裝置的[硬體安全模組 (HSM)](https://azure.microsoft.com/blog/azure-iot-supports-new-security-hardware-to-strengthen-iot-security) 為裝置設定裝置佈建服務，並讓裝置可以在首次開機時連線到裝置佈建服務。 本教學課程會討論下列作業的程序：

> [!div class="checklist"]
> * 選取硬體安全模組
> * 為選定的 HSM 建置裝置佈建用戶端 SDK
> * 擷取安全構件
> * 在裝置上設定裝置佈建服務組態

## <a name="prerequisites"></a>必要條件

在繼續之前，請先使用[為雲端設定裝置佈建功能](./tutorial-set-up-cloud.md)教學課程中所提到的指示，建立裝置佈建服務執行個體和 IoT 中樞。


## <a name="select-a-hardware-security-module"></a>選取硬體安全模組

[裝置佈建服務用戶端 SDK](https://github.com/Azure/azure-iot-sdk-c/tree/master/provisioning_client) 可支援兩種硬體安全模組 (簡稱 HSM)： 

- [信賴平台模組 (TPM)](https://en.wikipedia.org/wiki/Trusted_Platform_Module)。
    - TPM 是適用於大部分 Windows 裝置平台以及一些 Linux/Ubuntu 架構裝置的公認標準。 身為裝置製造商，如果您的裝置是執行上述任一作業系統，而且您想要使用公認的 HSM 標準，則可以選擇這個 HSM。 若使用 TPM 晶片，裝置就只能個別地向裝置佈建服務進行註冊。 若要進行開發，您可以在 Windows 或 Linux 開發機器上使用 TPM 模擬器。

- [X.509](https://cryptography.io/en/latest/x509/) 架構的硬體安全模組。 
    - X.509 架構的 HSM 是較新型的晶片，Microsoft 目前正著手設計 RIoT 或 DICE 晶片以便實作 X.509 憑證。 若使用 X.509 晶片，您將可以在入口網站中進行大量註冊。 這種晶片也支援某些非 Windows 的作業系統，例如 embedOS。 針對開發用途，裝置佈建服務用戶端 SDK 可支援 X.509 裝置模擬器。 

身為裝置製造商，您必須選取以上述任一類型為基礎的硬體安全模組/晶片。 裝置佈建服務用戶端 SDK 目前不支援其他類型的 HSM。   


## <a name="build-device-provisioning-client-sdk-for-the-selected-hsm"></a>為選定的 HSM 建置裝置佈建用戶端 SDK

裝置佈建服務用戶端 SDK 可協助您在軟體中實作選定的安全性機制。 下列步驟說明如何使用選定 HSM 晶片的 SDK：

1. 如果您有遵循[建立模擬裝置的快速入門](./quick-create-simulated-device.md)，您就已設定妥當而可建置 SDK。 如果沒有，請遵循[準備開發環境](./quick-create-simulated-device.md#setupdevbox)一節的前四個步驟。 這四個步驟會複製裝置佈建服務用戶端 SDK 的 GitHub 存放庫，並安裝 `cmake` 建置工具。 

1. 在命令提示字元上使用下列其中一個命令，針對您為裝置選定的 HSM 類型建置 SDK：
    - 針對 TPM 裝置：
        ```cmd/sh
        cmake -Duse_prov_client:BOOL=ON ..
        ```

    - 針對 TPM 模擬器：
        ```cmd/sh
        cmake -Duse_prov_client:BOOL=ON -Duse_tpm_simulator:BOOL=ON ..
        ```

    - 針對 X.509 裝置和模擬器：
        ```cmd/sh
        cmake -Duse_prov_client:BOOL=ON ..
        ```

1. 針對執行了 Windows 或 Ubuntu 系統以實作 TPM 和 X.509 HSM 的裝置，SDK 會提供預設的支援。 請針對這些受支援的 HSM 繼續進行下面的[擷取安全構件](#extractsecurity)一節。 
 
## <a name="support-custom-tpm-and-x509-devices"></a>支援自訂的 TPM 和 X.509 裝置

對於並非執行 Windows 或 Ubuntu 的 TPM 和 X.509 裝置，裝置佈建系統用戶端 SDK 不會提供預設支援。 對於這類裝置，您必須為您特殊的 HSM 晶片撰寫自訂程式碼，如下列步驟所示：

### <a name="develop-your-custom-repository"></a>開發自訂存放庫

1. 開發程式庫來存取您的 HSM。 此專案必須產生靜態程式庫以供裝置佈建 SDK 取用。
1. 程式庫必須實作下列標頭檔所定義的函式：a. 實作自訂的 TPM 中定義的函式[自訂的 HSM 文件](https://github.com/Azure/azure-iot-sdk-c/blob/master/provisioning_client/devdoc/using_custom_hsm.md#hsm-tpm-api)。
    b. 實作自訂的 X.509 中定義的函式[自訂的 HSM 文件](https://github.com/Azure/azure-iot-sdk-c/blob/master/provisioning_client/devdoc/using_custom_hsm.md#hsm-x509-api)。 

### <a name="integrate-with-the-device-provisioning-service-client"></a>與裝置佈建服務用戶端整合

一旦您的程式庫已成功建置它自己，您可以移動到 iot 中樞 C-SDK，並針對您的程式庫連結：

1. 在下列 cmake 命令中提供自訂的 HSM GitHub 存放庫、程式庫路徑和其名稱：
    ```cmd/sh
    cmake -Duse_prov_client:BOOL=ON -Dhsm_custom_lib=<path_and_name_of_library> <PATH_TO_AZURE_IOT_SDK>
    ```
   
1. 在 Visual Studio 中開啟 SDK 並加以建置。 

    - 在建置程序將會編譯 SDK 程式庫。
    - SDK 會嘗試與 cmake 命令中所定義的自訂 HSM 進行連結。

1. 執行 `\azure-iot-sdk-c\provisioning_client\samples\prov_dev_client_ll_sample\prov_dev_client_ll_sample.c` 範例，以確認 HSM 是否有正確地實作。

<a id="extractsecurity"></a>
## <a name="extract-the-security-artifacts"></a>擷取安全構件

下一個步驟是在裝置上擷取 HSM 的安全構件。

1. 若為 TPM 裝置，您必須從 TPM 晶片製造商那邊找出其相關聯的**簽署金鑰**。 您可以將簽署金鑰進行雜湊處理，以衍生 TPM 裝置的唯一**註冊識別碼**。 
2. 若為 X.509 裝置，您必須取得對裝置所核發的憑證，也就是用來註冊個別裝置的終端實體憑證，以及用來以群組方式註冊裝置的根憑證。

您必須有這些安全構件才能向裝置佈建服務註冊裝置。 然後，佈建服務會等候這些裝置開機，並於稍後的任何時間點與裝置連線。 如需如何使用這些安全構件來建立註冊的相關資訊，請參閱[如何管理裝置註冊](how-to-manage-enrollments.md)。 

裝置第一次開機時，用戶端 SDK 會與晶片互動以從裝置擷取安全構件，並向裝置佈建服務確認註冊情形。 


## <a name="set-up-the-device-provisioning-service-configuration-on-the-device"></a>在裝置上設定裝置佈建服務組態

裝置製造程序的最後一個步驟是撰寫應用程式，以使用裝置佈建服務用戶端 SDK 來向服務註冊裝置。 這個 SDK 會提供下列 API 供應用程式使用：

```C
// Creates a Provisioning Client for communications with the Device Provisioning Client Service
PROV_DEVICE_LL_HANDLE Prov_Device_LL_Create(const char* uri, const char* scope_id, PROV_DEVICE_TRANSPORT_PROVIDER_FUNCTION protocol)

// Disposes of resources allocated by the provisioning Client.
void Prov_Device_LL_Destroy(PROV_DEVICE_LL_HANDLE handle)

// Asynchronous call initiates the registration of a device.
PROV_DEVICE_RESULT Prov_Device_LL_Register_Device(PROV_DEVICE_LL_HANDLE handle, PROV_DEVICE_CLIENT_REGISTER_DEVICE_CALLBACK register_callback, void* user_context, PROV_DEVICE_CLIENT_REGISTER_STATUS_CALLBACK reg_status_cb, void* status_user_ctext)

// Api to be called by user when work (registering device) can be done
void Prov_Device_LL_DoWork(PROV_DEVICE_LL_HANDLE handle)

// API sets a runtime option identified by parameter optionName to a value pointed to by value
PROV_DEVICE_RESULT Prov_Device_LL_SetOption(PROV_DEVICE_LL_HANDLE handle, const char* optionName, const void* value)
```

在使用這些 API 之前，請記得先依照[這個快速入門的＜模擬裝置的第一個開機順序＞章節](./quick-create-simulated-device.md#firstbootsequence)中的說明，將 `uri` 和 `id_scope` 變數初始化。 裝置佈建用戶端註冊 API `Prov_Device_LL_Create` 會連線至全域裝置佈建服務。 「識別碼範圍」會由服務產生，以保證唯一性。 識別碼範圍永遠不變，因此可用來唯一識別註冊識別碼。 `iothub_uri` 可讓 IoT 中樞用戶端註冊 API `IoTHubClient_LL_CreateFromDeviceAuth` 與正確的 IoT 中樞連線。 


這些 API 可協助裝置在開機時與裝置佈建服務進行連線和註冊，以取得 IoT 中樞的相關資訊，然後與其連線。 `provisioning_client/samples/prov_client_ll_sample/prov_client_ll_sample.c` 檔案會說明如何使用這些 API。 一般來說，您必須建立下列架構以註冊用戶端：

```C
static const char* global_uri = "global.azure-devices-provisioning.net";
static const char* id_scope = "[ID scope for your provisioning service]";
...
static void register_callback(DPS_RESULT register_result, const char* iothub_uri, const char* device_id, void* context)
{
    USER_DEFINED_INFO* user_info = (USER_DEFINED_INFO *)user_context;
    ...
    user_info. reg_complete = 1;
}
static void registation_status(DPS_REGISTRATION_STATUS reg_status, void* user_context)
{
}
int main()
{
    ...
    SECURE_DEVICE_TYPE hsm_type;
    hsm_type = SECURE_DEVICE_TYPE_TPM;
    //hsm_type = SECURE_DEVICE_TYPE_X509;
    prov_dev_security_init(hsm_type); // initialize your HSM 

    prov_transport = Prov_Device_HTTP_Protocol;
    
    PROV_CLIENT_LL_HANDLE handle = Prov_Device_LL_Create(global_uri, id_scope, prov_transport); // Create your provisioning client

    if (Prov_Client_LL_Register_Device(handle, register_callback, &user_info, register_status, &user_info) == IOTHUB_DPS_OK) {
        do {
        // The register_callback is called when registration is complete or fails
            Prov_Client_LL_DoWork(handle);
        } while (user_info.reg_complete == 0);
    }
    Prov_Client_LL_Destroy(handle); // Clean up the Provisioning client
    ...
    iothub_client = IoTHubClient_LL_CreateFromDeviceAuth(user_info.iothub_uri, user_info.device_id, transport); // Create your IoT hub client and connect to your hub
    ...
}
```

您可以使用測試服務安裝程式，先以模擬裝置改進裝置佈建服務用戶端註冊應用程式。 當應用程式可以在測試環境中運作後，您可以針對特定裝置來建置此應用程式，並將可執行檔複製到裝置映像中。 先不要啟動裝置，在啟動裝置之前，您必須先[向裝置佈建服務註冊裝置](./tutorial-provision-device-to-hub.md#enrolldevice)。 請參閱後續步驟以了解此程序。 

## <a name="clean-up-resources"></a>清除資源

至此，您可能已在入口網站中設定裝置佈建和 IoT 中樞服務。 如果您想要放棄裝置佈建設定及 (或) 延遲使用這些服務，建議您將其關閉以避免產生不必要的成本。

1. 從 Azure 入口網站的左側功能表中，按一下 [所有資源]，然後選取您的裝置佈建服務。 在 [所有資源] 刀鋒視窗的頂端，按一下 [刪除]。  
1. 從 Azure 入口網站的左側功能表中，按一下 [所有資源]，然後選取您的 IoT 中樞。 在 [所有資源] 刀鋒視窗的頂端，按一下 [刪除]。  


## <a name="next-steps"></a>後續步驟
在本教學課程中，您已了解如何：

> [!div class="checklist"]
> * 選取硬體安全模組
> * 為選定的 HSM 建置裝置佈建用戶端 SDK
> * 擷取安全構件
> * 在裝置上設定裝置佈建服務組態

前進到下一個教學課程，以了解如何藉由向 Azure IoT 中樞裝置佈建服務註冊要讓裝置進行自動佈建，來將裝置佈建到 IoT 中樞。

> [!div class="nextstepaction"]
> [將裝置佈建到 IoT 中樞](tutorial-provision-device-to-hub.md)

