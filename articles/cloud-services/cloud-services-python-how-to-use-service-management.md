---
title: "aaaHow toouse hello 服務管理 API (Python)-功能指南"
description: "了解如何 tooprogrammatically 來自 Python 執行服務的一般管理工作。"
services: cloud-services
documentationcenter: python
author: lmazuel
manager: wpickett
editor: 
ms.assetid: 61538ec0-1536-4a7e-ae89-95967fe35d73
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/30/2017
ms.author: lmazuel
ms.openlocfilehash: b59622203470e1586484cec4033515edb39ca4d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-management-from-python"></a>如何 toouse 來自 Python 的服務管理
本指南也說明如何 tooprogrammatically 來自 Python 執行服務的一般管理工作。 hello **ServiceManagementService**類別中 hello [Azure SDK for Python](https://github.com/Azure/azure-sdk-for-python)支援以程式設計方式存取 toomuch 的 hello 服務管理相關的功能所提供之 hello [Azure 傳統入口網站][ management-portal] (例如**建立、 更新和刪除雲端服務、 部署、 資料管理服務和虛擬機器**)。 這項功能可用於建置需要以程式設計方式存取 tooservice 管理的應用程式。

## <a name="WhatIs"> </a>什麼是服務管理？
hello 服務管理 API 提供以程式設計方式存取 toomuch 的 hello 服務管理功能可透過 hello [Azure 傳統入口網站][management-portal]。 hello Azure SDK for Python 可讓您 toomanage 雲端服務和儲存體帳戶。

toouse hello 服務管理 API，您需要太[建立 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="Concepts"> </a>概念
hello Azure SDK for Python 包裝 hello [Azure 服務管理 API][svc-mgmt-rest-api]，這是 REST API。 所有 API 作業都會透過 SSL 而執行，並可使用 X.509 v3 憑證相互驗證。 hello 管理服務可能會從執行在 Azure 中，或直接透過 hello 網際網路從可以傳送 HTTPS 要求和接收 HTTPS 回應的應用程式的服務內存取。

## <a name="Installation"> </a>安裝
本文中所述的所有 hello 功能都都可以在 hello`azure-servicemanagement-legacy`封裝，您可以安裝使用 pip。 如需安裝 （例如，如果您是新 tooPython） 的詳細資訊，請參閱這篇文章：[安裝 Python 和 hello Azure SDK](../python-how-to-install.md)

## <a name="Connect"></a>How to: tooservice management 連接
tooconnect toohello 服務管理端點，您需要 Azure 訂用帳戶 ID 和有效的管理憑證。 您可以取得您的訂用帳戶 ID，透過 hello [Azure 傳統入口網站][management-portal]。

> [!NOTE]
> 它現在是在 Windows 上執行時使用 OpenSSL 建立可能 toouse 憑證。  這需要使用 Python 2.7.4 或更新版本。 我們建議使用者 toouse OpenSSL 而不是.pfx，因為.pfx 憑證很可能會移除 hello 未來的支援。
>
>

### <a name="management-certificates-on-windowsmaclinux-openssl"></a>Windows/Mac/Linux 上的管理憑證 (OpenSSL)
您可以使用[OpenSSL](http://www.openssl.org/) toocreate 管理憑證。  實際需要 toocreate 兩個憑證，一個用於 hello 伺服器 (`.cer`檔案)，另一個用於 hello 用戶端 (`.pem`檔案)。 toocreate hello`.pem`檔案中，執行：

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

toocreate hello`.cer`憑證，請執行：

    openssl x509 -inform pem -in mycert.pem -outform der -out mycert.cer

如需有關 Azure 憑證的詳細資訊，請參閱 [Azure 雲端服務的憑證概觀](cloud-services-certs-create.md)。 OpenSSL 參數的完整說明，請參閱 hello 文件，網址[http://www.openssl.org/docs/apps/openssl.html](http://www.openssl.org/docs/apps/openssl.html)。

您已建立這些檔案之後，您需要 tooupload hello`.cer`檔案透過 hello hello hello [設定] 索引標籤的 [上傳 」 動作 tooAzure [Azure 傳統入口網站][management-portal]，而且您需要 toomake 記下您用來儲存 hello`.pem`檔案。

取得訂用帳戶 ID 之後，建立憑證，並上傳 hello`.cer`檔案 tooAzure，您可以藉由傳遞 hello 訂用帳戶 id 和 hello 路徑 toohello 連接 toohello Azure 的管理端點`.pem`檔案太**ServiceManagementService**:

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = '<path_to_.pem_certificate>'

    sms = ServiceManagementService(subscription_id, certificate_path)

在上述範例中，hello`sms`是**ServiceManagementService**物件。 hello **ServiceManagementService**類別是 hello 所使用的主要類別 toomanage Azure 服務。

### <a name="management-certificates-on-windows-makecert"></a>Windows 上的管理憑證 (MakeCert)
您可以使用 `makecert.exe`，在您的機器上建立自我簽署管理憑證。  開啟**Visual Studio 命令提示字元**為**管理員**並使用下列命令、 取代 hello *AzureCertificate*具有您想要的 hello 憑證名稱toouse。

    makecert -sky exchange -r -n "CN=AzureCertificate" -pe -a sha1 -len 2048 -ss My "AzureCertificate.cer"

hello 命令會建立 hello`.cer`檔案，並將它安裝在 hello**個人**憑證存放區。 如需詳細資訊，請參閱 [Azure 雲端服務的憑證概觀](cloud-services-certs-create.md)。

您已建立 hello 憑證之後，您需要 tooupload hello`.cer`檔案透過 hello hello hello [設定] 索引標籤的 [上傳 」 動作 tooAzure [Azure 傳統入口網站][management-portal]。

取得訂用帳戶 ID 之後，建立憑證，並上傳 hello`.cer`檔案 tooAzure，您可以連接 toohello Azure 的管理端點 hello 訂用帳戶 id 和憑證 hello hello 位置傳入您**個人**太憑證存放區**ServiceManagementService** (同樣地，取代*AzureCertificate* hello 名稱，為您的憑證):

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = 'CURRENT_USER\\my\\AzureCertificate'

    sms = ServiceManagementService(subscription_id, certificate_path)

在上述範例中，hello`sms`是**ServiceManagementService**物件。 hello **ServiceManagementService**類別是 hello 所使用的主要類別 toomanage Azure 服務。

## <a name="ListAvailableLocations"> </a>作法：列出可用位置
toolist hello 位置可供主機服務，使用 hello**清單\_位置**方法：

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_locations()
    for location in result:
        print(location.name)

當您建立雲端服務或儲存體服務會需要 tooprovide 有效的位置。 hello**清單\_位置**方法一律會傳回最新的 hello 目前可用的位置清單。 在撰寫本文 hello 可用的位置是：

* 西歐
* 北歐
* 東南亞
* 東亞
* 美國中部
* 美國中北部
* 美國中南部
* 美國西部
* 美國東部
* 日本東部
* 日本西部
* 巴西南部
* 澳洲東部
* 澳大利亞東南部

## <a name="CreateCloudService"> </a>作法：建立雲端服務
當您建立應用程式，並在 Azure 中執行它，hello 程式碼和組態併稱為 Azure[雲端服務][ cloud service] (又稱為*託管服務*中稍早Azure 版本）。 hello**建立\_裝載\_服務**方法可讓您 toocreate 新的託管服務提供的託管的服務名稱 （這必須是在 Azure 中是唯一的），標籤 (自動編碼 toobase64)，描述和位置。

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myhostedservice'
    label = 'myhostedservice'
    desc = 'my hosted service'
    location = 'West US'

    sms.create_hosted_service(name, label, desc, location)

您可以列出所有 hello 託管服務訂用帳戶以 hello**都清單\_裝載\_服務**方法：

    result = sms.list_hosted_services()

    for hosted_service in result:
        print('Service name: ' + hosted_service.service_name)
        print('Management URL: ' + hosted_service.url)
        print('Location: ' + hosted_service.hosted_service_properties.location)
        print('')

如果您想 tooget 特定託管服務的資訊，您可以藉由傳遞 hello 託管服務名稱 toohello**取得\_裝載\_服務\_屬性**方法：

    hosted_service = sms.get_hosted_service_properties('myhostedservice')

    print('Service name: ' + hosted_service.service_name)
    print('Management URL: ' + hosted_service.url)
    print('Location: ' + hosted_service.hosted_service_properties.location)

您已建立雲端服務之後，您可以部署您的程式碼 toohello 服務以 hello**建立\_部署**方法。

## <a name="DeleteCloudService"> </a>作法：刪除雲端服務
您可以刪除雲端服務，藉由傳遞 hello 服務名稱 toohello**刪除\_裝載\_服務**方法：

    sms.delete_hosted_service('myhostedservice')

您可以刪除服務之前，必須先刪除所有部署的 hello 服務。 (請參閱 [作法：刪除部署](#DeleteDeployment) ，以取得詳細資料)。

## <a name="DeleteDeployment"> </a>作法：刪除部署
toodelete 部署中，使用 hello**刪除\_部署**方法。 hello 下列範例示範如何 toodelete 部署名為`v1`。

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment('myhostedservice', 'v1')

## <a name="CreateStorageService"> </a>作法：建立儲存體服務
A[儲存體服務](../storage/common/storage-create-storage-account.md)可讓您存取 tooAzure [Blob](../storage/blobs/storage-python-how-to-use-blob-storage.md)，[資料表](../cosmos-db/table-storage-how-to-use-python.md)，和[佇列](../storage/queues/storage-python-how-to-use-queue-storage.md)。 toocreate 儲存體服務，您需要 hello 服務 （介於 3 到 24 個小寫字元和在 Azure 中獨一無二） 的名稱、 描述、 標籤 （向上 too100 字元，會自動編碼 toobase64） 和位置。 hello 下列範例顯示如何 toocreate 儲存體服務所指定的位置。

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'mystorageaccount'
    label = 'mystorageaccount'
    location = 'West US'
    desc = 'My storage account description.'

    result = sms.create_storage_account(name, desc, label, location=location)

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

請注意在上述範例中的 hello hello hello 狀態**建立\_儲存體\_帳戶**作業可以藉由傳遞傳回 hello 結果擷取**建立\_儲存體\_帳戶**toohello**取得\_作業\_狀態**方法。  

您可以列出儲存體帳戶和其屬性與 hello**清單\_儲存體\_帳戶**方法：

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_storage_accounts()
    for account in result:
        print('Service name: ' + account.service_name)
        print('Location: ' + account.storage_service_properties.location)
        print('')

## <a name="DeleteStorageService"> </a>作法：刪除儲存體服務
您可以刪除儲存體服務藉由傳遞 hello 儲存體服務名稱 toohello**刪除\_儲存體\_帳戶**方法。 刪除儲存體服務刪除儲存在 hello 服務 （blob、 資料表和佇列） 中的所有資料。

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_storage_account('mystorageaccount')

## <a name="ListOperatingSystems"> </a>作法：列出可用作業系統
toolist hello 作業系統可供主機服務，會使用 hello**清單\_操作\_系統**方法：

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_operating_systems()

    for os in result:
        print('OS: ' + os.label)
        print('Family: ' + os.family_label)
        print('Active: ' + str(os.is_active))

或者，您可以使用 hello**清單\_操作\_系統\_系列**方法，以分組 hello 作業系統系列：

    result = sms.list_operating_system_families()

    for family in result:
        print('Family: ' + family.label)
        for os in family.operating_systems:
            if os.is_active:
                print('OS: ' + os.label)
                print('Version: ' + os.version)
        print('')

## <a name="CreateVMImage"> </a>作法：建立作業系統映像
tooadd 作業系統映像 toohello 映像儲存機制，使用 hello**新增\_os\_映像**方法：

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'mycentos'
    label = 'mycentos'
    os = 'Linux' # Linux or Windows
    media_link = 'url_to_storage_blob_for_source_image_vhd'

    result = sms.add_os_image(label, media_link, name, os)

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

toolist hello 作業系統提供的映像，使用 hello**清單\_os\_映像**方法。 其中包括所有的平台映像和使用者映像：

    result = sms.list_os_images()

    for image in result:
        print('Name: ' + image.name)
        print('Label: ' + image.label)
        print('OS: ' + image.os)
        print('Category: ' + image.category)
        print('Description: ' + image.description)
        print('Location: ' + image.location)
        print('Media link: ' + image.media_link)
        print('')

## <a name="DeleteVMImage"> </a>作法：刪除作業系統映像
toodelete 使用者映像使用 hello**刪除\_os\_映像**方法：

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.delete_os_image('mycentos')

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

## <a name="CreateVM"> </a>作法：建立虛擬機器
toocreate 虛擬機器，您必須先 toocreate[雲端服務](#CreateCloudService)。  然後，建立使用 hello hello 虛擬機器部署**建立\_虛擬\_機器\_部署**方法：

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myvm'
    location = 'West US'

    #Set hello location
    sms.create_hosted_service(service_name=name,
        label=name,
        location=location)

    # Name of an os image as returned by list_os_images
    image_name = 'OpenLogic__OpenLogic-CentOS-62-20120531-en-us-30GB.vhd'

    # Destination storage account container/blob where hello VM disk
    # will be created
    media_link = 'url_to_target_storage_blob_for_vm_hd'

    # Linux VM configuration, you can use WindowsConfigurationSet
    # for a Windows VM instead
    linux_config = LinuxConfigurationSet('myhostname', 'myuser', 'mypassword', True)

    os_hd = OSVirtualHardDisk(image_name, media_link)

    sms.create_virtual_machine_deployment(service_name=name,
        deployment_name=name,
        deployment_slot='production',
        label=name,
        role_name=name,
        system_config=linux_config,
        os_virtual_hard_disk=os_hd,
        role_size='Small')

## <a name="DeleteVM"> </a>作法：刪除虛擬機器
toodelete 虛擬機器，您先刪除使用 hello hello 部署**刪除\_部署**方法：

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment(service_name='myvm',
        deployment_name='myvm')

hello 刪除雲端服務可以接著使用 hello**刪除\_裝載\_服務**方法：

    sms.delete_hosted_service(service_name='myvm')

## <a name="how-to-create-a-virtual-machine-from-a-captured-virtual-machine-image"></a>作法：從擷取的虛擬機器映像建立虛擬機器
toocapture VM 映像，您先呼叫 hello**擷取\_vm\_映像**方法：

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    # replace hello below three parameters with actual values
    hosted_service_name = 'hs1'
    deployment_name = 'dep1'
    vm_name = 'vm1'

    image_name = vm_name + 'image'
    image = CaptureRoleAsVMImage    ('Specialized',
        image_name,
        image_name + 'label',
        image_name + 'description',
        'english',
        'mygroup')

    result = sms.capture_vm_image(
            hosted_service_name,
            deployment_name,
            vm_name,
            image
        )

接下來，確定您已成功擷取 hello 映像，請使用 hello 的 toomake**清單\_vm\_映像**應用程式開發介面，並確定您的映像，都會在 hello 結果：

    images = sms.list_vm_images()

toofinally hello 使用建立虛擬機器 hello 擷取的映像，請使用 hello**建立\_虛擬\_機器\_部署**方法，如往常一般，但這次傳入 hello vm_image_name 改為

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myvm'
    location = 'West US'

    #Set hello location
    sms.create_hosted_service(service_name=name,
        label=name,
        location=location)

    sms.create_virtual_machine_deployment(service_name=name,
        deployment_name=name,
        deployment_slot='production',
        label=name,
        role_name=name,
        system_config=linux_config,
        os_virtual_hard_disk=None,
        role_size='Small',
        vm_image_name = image_name)

toolearn 深入了解如何 toocapture Linux 虛擬機器，請參閱[如何 tooCapture Linux 虛擬機器。](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

toolearn 深入了解如何 toocapture Windows 虛擬機器，請參閱[如何 tooCapture Windows 虛擬機器。](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="What's Next"> </a>後續步驟
現在，您學到的服務管理的 hello 基本概念，您可以存取 hello [hello Azure Python SDK 的完整的 API 參考文件](http://azure-sdk-for-python.readthedocs.org/)並執行複雜工作輕鬆 toomanage python 應用程式。

如需詳細資訊，請參閱 hello [Python 開發人員中心](/develop/python/)。

[What is Service Management]: #WhatIs
[Concepts]: #Concepts
[How to: Connect tooservice management]: #Connect
[How to: List available locations]: #ListAvailableLocations
[How to: Create a cloud service]: #CreateCloudService
[How to: Delete a cloud service]: #DeleteCloudService
[How to: Create a deployment]: #CreateDeployment
[How to: Update a deployment]: #UpdateDeployment
[How to: Move deployments between staging and production]: #MoveDeployments
[How to: Delete a deployment]: #DeleteDeployment
[How to: Create a storage service]: #CreateStorageService
[How to: Delete a storage service]: #DeleteStorageService
[How to: List available operating systems]: #ListOperatingSystems
[How to: Create an operating system image]: #CreateVMImage
[How to: Delete an operating system image]: #DeleteVMImage
[How to: Create a virtual machine]: #CreateVM
[How to: Delete a virtual machine]: #DeleteVM
[Next Steps]: #NextSteps
[management-portal]: https://manage.windowsazure.com/
[svc-mgmt-rest-api]: http://msdn.microsoft.com/library/windowsazure/ee460799.aspx


[cloud service]:/services/cloud-services/
