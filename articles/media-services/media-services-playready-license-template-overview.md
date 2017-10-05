---
title: "媒體服務 PlayReady 授權範本概觀"
description: "本主題提供了用來設定 PlayReady 授權之 PlayReady 授權範本的概觀。"
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: fddce5d0-1278-478f-ae05-9b985c748731
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: be19f616e36916655390cd05e738e93c08dcdf68
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="media-services-playready-license-template-overview"></a><span data-ttu-id="03377-103">媒體服務 PlayReady 授權範本概觀</span><span class="sxs-lookup"><span data-stu-id="03377-103">Media Services PlayReady license template overview</span></span>
<span data-ttu-id="03377-104">Azure 媒體服務現在提供一種服務，來傳遞 Microsoft PlayReady 授權。</span><span class="sxs-lookup"><span data-stu-id="03377-104">Azure Media Services now provides a service for delivering Microsoft PlayReady licenses.</span></span> <span data-ttu-id="03377-105">使用者播放程式 (例如 Silverlight) 嘗試播放 PlayReady 保護內容時，會將要求傳送到授權傳遞服務來取得授權。</span><span class="sxs-lookup"><span data-stu-id="03377-105">When the end user player (for example, Silverlight) tries to play your PlayReady protected content, a request is sent to the license delivery service to obtain a license.</span></span> <span data-ttu-id="03377-106">如果授權服務核准要求，就會發出傳送給用戶端並可用來解密和播放所指定內容的授權。</span><span class="sxs-lookup"><span data-stu-id="03377-106">If the license service approves the request, it issues the license which is sent to the client and can be used to decrypt and play the specified content.</span></span>

<span data-ttu-id="03377-107">媒體服務也會提供可讓您設定 PlayReady 授權的 API。</span><span class="sxs-lookup"><span data-stu-id="03377-107">Media Services also provides APIs that let you configure your PlayReady licenses.</span></span> <span data-ttu-id="03377-108">授權包含您要 PlayReady DRM 執行階段在使用者嘗試播放受保護內容時強制執行的權限和限制。</span><span class="sxs-lookup"><span data-stu-id="03377-108">Licenses contain the rights and restrictions that you want for the PlayReady DRM runtime to enforce when a user is trying to playback protected content.</span></span>
<span data-ttu-id="03377-109">以下是您可以指定之 PlayReady 授權限制的一些範例：</span><span class="sxs-lookup"><span data-stu-id="03377-109">Below are some examples of PlayReady license restrictions that you can specify:</span></span>

* <span data-ttu-id="03377-110">授權從此時間期間起有效的 DateTime。</span><span class="sxs-lookup"><span data-stu-id="03377-110">The DateTime from which the license is valid.</span></span>
* <span data-ttu-id="03377-111">授權過期的 DateTime 值。</span><span class="sxs-lookup"><span data-stu-id="03377-111">The DateTime value when the license expires.</span></span> 
* <span data-ttu-id="03377-112">針對要儲存在用戶端上永續性儲存體的授權。</span><span class="sxs-lookup"><span data-stu-id="03377-112">For the license to be saved in persistent storage on the client.</span></span> <span data-ttu-id="03377-113">永續性授權通常會用來允許離線播放內容。</span><span class="sxs-lookup"><span data-stu-id="03377-113">Persistent licenses are typically used to allow offline playback of the content.</span></span>
* <span data-ttu-id="03377-114">播放器播放您的內容必須具有的最低安全性層級。</span><span class="sxs-lookup"><span data-stu-id="03377-114">The minimum security level that a player must have to play your content.</span></span> 
* <span data-ttu-id="03377-115">audio\video 內容的輸出控制輸出保護層級。</span><span class="sxs-lookup"><span data-stu-id="03377-115">The output protection level for the output controls for audio\video content.</span></span> 
* <span data-ttu-id="03377-116">如需詳細資訊，請參閱 [PlayReady 法規規則](https://www.microsoft.com/playready/licensing/compliance/) 文件中的「輸出控制」區段 (3.5)。</span><span class="sxs-lookup"><span data-stu-id="03377-116">For more information, see the Output Controls section (3.5) in the [PlayReady Compliance Rules](https://www.microsoft.com/playready/licensing/compliance/) document.</span></span>

> [!NOTE]
> <span data-ttu-id="03377-117">目前，您只能設定 PlayReady 授權的 PlayRight (這是必要權限)。</span><span class="sxs-lookup"><span data-stu-id="03377-117">Currently, you can only configure the PlayRight of the PlayReady license (this right is required).</span></span> <span data-ttu-id="03377-118">PlayRight 可讓用戶端播放內容。</span><span class="sxs-lookup"><span data-stu-id="03377-118">The PlayRight gives the client the ability to playback the content.</span></span> <span data-ttu-id="03377-119">PlayRight 也可讓設定限制專屬於播放。</span><span class="sxs-lookup"><span data-stu-id="03377-119">The PlayRight also allows configuring restrictions specific to playback.</span></span> <span data-ttu-id="03377-120">如需詳細資訊，請參閱 [PlayReadyPlayRight](media-services-playready-license-template-overview.md#PlayReadyPlayRight)。</span><span class="sxs-lookup"><span data-stu-id="03377-120">For more information, see [PlayReadyPlayRight](media-services-playready-license-template-overview.md#PlayReadyPlayRight).</span></span>
> 
> 

<span data-ttu-id="03377-121">若要使用媒體服務設定 PlayReady 授權，您必須設定媒體服務 PlayReady 授權範本。</span><span class="sxs-lookup"><span data-stu-id="03377-121">To configure PlayReady licenses using Media Services, you must configure the Media Services PlayReady license template.</span></span> <span data-ttu-id="03377-122">範本會在 XML 中定義。</span><span class="sxs-lookup"><span data-stu-id="03377-122">The template is defined in XML.</span></span>

<span data-ttu-id="03377-123">下列範例顯示設定基本串流授權的最簡單 (也是最常見) 範本。</span><span class="sxs-lookup"><span data-stu-id="03377-123">The following example shows the simplest (and most common) template that configures a basic streaming license.</span></span> <span data-ttu-id="03377-124">使用此授權，您的用戶端就可以播放您的 PlayReady 受保護內容。</span><span class="sxs-lookup"><span data-stu-id="03377-124">With this license, your clients would be able to playback your PlayReady protected content.</span></span>

    <?xml version="1.0" encoding="utf-8"?>
    <PlayReadyLicenseResponseTemplate xmlns:i="http://www.w3.org/2001/XMLSchema-instance" 
                                      xmlns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1">
      <LicenseTemplates>
        <PlayReadyLicenseTemplate>
          <ContentKey i:type="ContentEncryptionKeyFromHeader" />
          <PlayRight />
        </PlayReadyLicenseTemplate>
      </LicenseTemplates>
    </PlayReadyLicenseResponseTemplate>

<span data-ttu-id="03377-125">XML 符合 PlayReady 授權範本 XML 結構描述，該結構描述是在 PlayReady 授權範本 XML 結構描述區段中定義。</span><span class="sxs-lookup"><span data-stu-id="03377-125">The XML conforms to the PlayReady license template XML schema defined in the PlayReady license template XML schema section.</span></span>

<span data-ttu-id="03377-126">媒體服務也會定義一組可以用來在 XML 中序列化和還原序列化的 .NET 類別。</span><span class="sxs-lookup"><span data-stu-id="03377-126">Media Services also defines a set of .NET classes that could be used to serialized and deserialized to and from the XML.</span></span> <span data-ttu-id="03377-127">對於主要類別的描述，請參閱 [媒體服務 .NET 類別](media-services-playready-license-template-overview.md#classes)。</span><span class="sxs-lookup"><span data-stu-id="03377-127">For description of main classes, see [Media Services .NET classes](media-services-playready-license-template-overview.md#classes).</span></span> <span data-ttu-id="03377-128">其作用是設定授權範本。</span><span class="sxs-lookup"><span data-stu-id="03377-128">that are used to configure license templates.</span></span>

<span data-ttu-id="03377-129">如需使用 .NET 類別來設定 PlayReady 授權範本的端對端範例，請參閱 [使用 PlayReady 動態加密和授權傳遞服務](media-services-protect-with-drm.md)。</span><span class="sxs-lookup"><span data-stu-id="03377-129">For an end-to-end example that uses .NET classes to configure the PlayReady license template, see [Using PlayReady Dynamic Encryption and License Delivery Service](media-services-protect-with-drm.md).</span></span>

## <span data-ttu-id="03377-130"><a id="classes"></a>用來設定授權範本的媒體服務 .NET 類別</span><span class="sxs-lookup"><span data-stu-id="03377-130"><a id="classes"></a>Media Services .NET classes that are used to configure license templates</span></span>
<span data-ttu-id="03377-131">以下是主要的 .NET 類別，可用於設定媒體服務 PlayReady 授權範本。</span><span class="sxs-lookup"><span data-stu-id="03377-131">The following are the main .NET classes are used to configure Media Services PlayReady license templates.</span></span> <span data-ttu-id="03377-132">這些類別對應至 [PlayReady 授權範本 XML 結構描述](media-services-playready-license-template-overview.md#schema)中定義的類型。</span><span class="sxs-lookup"><span data-stu-id="03377-132">These classes map to the types defined in [PlayReady license template XML schema](media-services-playready-license-template-overview.md#schema).</span></span>

<span data-ttu-id="03377-133">[MediaServicesLicenseTemplateSerializer](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.mediaserviceslicensetemplateserializer.aspx) 類別是用來序列化和還原序列化媒體服務授權範本 XML。</span><span class="sxs-lookup"><span data-stu-id="03377-133">The [MediaServicesLicenseTemplateSerializer](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.mediaserviceslicensetemplateserializer.aspx) class is used to serialize and deserialize to and from the Media Services license template XML.</span></span>

### <a name="playreadylicenseresponsetemplate"></a><span data-ttu-id="03377-134">PlayReadyLicenseResponseTemplate</span><span class="sxs-lookup"><span data-stu-id="03377-134">PlayReadyLicenseResponseTemplate</span></span>
<span data-ttu-id="03377-135">[PlayReadyLicenseResponseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicenseresponsetemplate.aspx) - 此類別代表傳回給使用者之回應的範本。</span><span class="sxs-lookup"><span data-stu-id="03377-135">[PlayReadyLicenseResponseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicenseresponsetemplate.aspx) - This class represents the template for the response sent back to the end user.</span></span> <span data-ttu-id="03377-136">它包含授權伺服器與應用程式之間的自訂資料字串的欄位 (對於自訂應用程式邏輯很有用)，以及一或多個授權範本的清單。</span><span class="sxs-lookup"><span data-stu-id="03377-136">It contains a field for a custom data string between the license server and the application (may be useful for custom app logic) as well as a list of one or more license templates.</span></span>

<span data-ttu-id="03377-137">這是範本階層中的「最上層」類別。</span><span class="sxs-lookup"><span data-stu-id="03377-137">This is the “top level” class in the template hierarchy.</span></span> <span data-ttu-id="03377-138">表示回應範本包含授權範本的清單，而授權範本包含 (直接或間接) 所有其他類別，這些類別組成要序列化的範本資料。</span><span class="sxs-lookup"><span data-stu-id="03377-138">Meaning that the response template includes a list of license templates and the license templates include (directly or indirectly) all of the other classes that make up the template data to be serialized.</span></span>

### <a name="playreadylicensetemplate"></a><span data-ttu-id="03377-139">PlayReadyLicenseTemplate</span><span class="sxs-lookup"><span data-stu-id="03377-139">PlayReadyLicenseTemplate</span></span>
<span data-ttu-id="03377-140">[PlayReadyLicenseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicensetemplate.aspx) - 類別代表用於建立 PlayReady 授權 (傳回給使用者) 的授權範本。</span><span class="sxs-lookup"><span data-stu-id="03377-140">[PlayReadyLicenseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicensetemplate.aspx) - The class represents a license template for creating PlayReady licenses to be returned to the end users.</span></span> <span data-ttu-id="03377-141">它包含授權中內容金鑰的資料，和使用內容金鑰時，由 PlayReady DRM 執行階段強制執行的任何權限和限制。</span><span class="sxs-lookup"><span data-stu-id="03377-141">It contains the data on the content key in the license and any rights or restrictions to be enforced by the PlayReady DRM runtime when using the content key.</span></span>

### <span data-ttu-id="03377-142"><a id="PlayReadyPlayRight"></a>PlayReadyPlayRight</span><span class="sxs-lookup"><span data-stu-id="03377-142"><a id="PlayReadyPlayRight"></a>PlayReadyPlayRight</span></span>
<span data-ttu-id="03377-143">[PlayReadyPlayRight](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadyplayright.aspx) - 此類別代表 PlayReady 授權的 PlayRight。</span><span class="sxs-lookup"><span data-stu-id="03377-143">[PlayReadyPlayRight](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadyplayright.aspx) - This class represents the PlayRight of a PlayReady license.</span></span> <span data-ttu-id="03377-144">它授與使用者能力可以播放內容，該內容受限於授權中設定及 PlayRight 本身 (適用於播放特定原則) 的零或多個限制。</span><span class="sxs-lookup"><span data-stu-id="03377-144">It grants the user the ability to playback the content subject to the zero or more restrictions configured in the license and on the PlayRight itself (for playback specific policy).</span></span> <span data-ttu-id="03377-145">大部分的 PlayRight 原則與輸出限制相關，控制內容可以播放的輸出類型，和使用指定輸出時必須套用的任何限制。</span><span class="sxs-lookup"><span data-stu-id="03377-145">Much of the policy on the PlayRight has to do with output restrictions which control the types of outputs that the content can be played over and any restrictions that must be put in place when using a given output.</span></span> <span data-ttu-id="03377-146">例如，如果 DigitalVideoOnlyContentRestriction 已啟用，則 DRM 執行階段只會允許透過數位輸出 (不允許類比視訊輸出傳遞內容) 顯示視訊。</span><span class="sxs-lookup"><span data-stu-id="03377-146">For example, if the DigitalVideoOnlyContentRestriction is enabled, then the DRM runtime will only allow the video to be displayed over digital outputs (analog video outputs won’t be allowed to pass the content).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="03377-147">這些類型的限制非常強大，但也可能會影響客戶體驗。</span><span class="sxs-lookup"><span data-stu-id="03377-147">These types of restrictions can be very powerful but can also affect the consumer experience.</span></span> <span data-ttu-id="03377-148">如果輸出保護設定限制太多，內容可能無法在某些用戶端上播放。</span><span class="sxs-lookup"><span data-stu-id="03377-148">If the output protections are configured too restrictive, the content might be unplayable on some clients.</span></span> <span data-ttu-id="03377-149">如需詳細資訊，請參閱 [PlayReady 法規規則](https://www.microsoft.com/playready/licensing/compliance/) 文件。</span><span class="sxs-lookup"><span data-stu-id="03377-149">For more information, see the [PlayReady Compliance Rules](https://www.microsoft.com/playready/licensing/compliance/) document.</span></span>
> 
> 

<span data-ttu-id="03377-150">如需 Silverlight 支援的保護層級的範例，請參閱： [Silverlight 支援輸出保護](http://go.microsoft.com/fwlink/?LinkId=617318)。</span><span class="sxs-lookup"><span data-stu-id="03377-150">For an example of what protection levels Silverlight supports, see: [Silverlight support for output protections](http://go.microsoft.com/fwlink/?LinkId=617318).</span></span>

## <span data-ttu-id="03377-151"><a id="schema"></a>PlayReady 授權範本 XML 結構描述</span><span class="sxs-lookup"><span data-stu-id="03377-151"><a id="schema"></a>PlayReady license template XML schema</span></span>
    <?xml version="1.0" encoding="utf-8"?>
    <xs:schema xmlns:tns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1" xmlns:ser="http://schemas.microsoft.com/2003/10/Serialization/" elementFormDefault="qualified" targetNamespace="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1" xmlns:xs="http://www.w3.org/2001/XMLSchema">
      <xs:import namespace="http://schemas.microsoft.com/2003/10/Serialization/" />
      <xs:complexType name="AgcAndColorStripeRestriction">
        <xs:sequence>
          <xs:element minOccurs="0" name="ConfigurationData" type="xs:unsignedByte" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="AgcAndColorStripeRestriction" nillable="true" type="tns:AgcAndColorStripeRestriction" />
      <xs:simpleType name="ContentType">
        <xs:restriction base="xs:string">
          <xs:enumeration value="Unspecified" />
          <xs:enumeration value="UltravioletDownload" />
          <xs:enumeration value="UltravioletStreaming" />
        </xs:restriction>
      </xs:simpleType>
      <xs:element name="ContentType" nillable="true" type="tns:ContentType" />
      <xs:complexType name="ExplicitAnalogTelevisionRestriction">
        <xs:sequence>
          <xs:element minOccurs="0" name="BestEffort" type="xs:boolean" />
          <xs:element minOccurs="0" name="ConfigurationData" type="xs:unsignedByte" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ExplicitAnalogTelevisionRestriction" nillable="true" type="tns:ExplicitAnalogTelevisionRestriction" />
      <xs:complexType name="PlayReadyContentKey">
        <xs:sequence />
      </xs:complexType>
      <xs:element name="PlayReadyContentKey" nillable="true" type="tns:PlayReadyContentKey" />
      <xs:complexType name="ContentEncryptionKeyFromHeader">
        <xs:complexContent mixed="false">
          <xs:extension base="tns:PlayReadyContentKey">
            <xs:sequence />
          </xs:extension>
        </xs:complexContent>
      </xs:complexType>
      <xs:element name="ContentEncryptionKeyFromHeader" nillable="true" type="tns:ContentEncryptionKeyFromHeader" />
      <xs:complexType name="ContentEncryptionKeyFromKeyIdentifier">
        <xs:complexContent mixed="false">
          <xs:extension base="tns:PlayReadyContentKey">
            <xs:sequence>
              <xs:element minOccurs="0" name="KeyIdentifier" type="ser:guid" />
            </xs:sequence>
          </xs:extension>
        </xs:complexContent>
      </xs:complexType>
      <xs:element name="ContentEncryptionKeyFromKeyIdentifier" nillable="true" type="tns:ContentEncryptionKeyFromKeyIdentifier" />
      <xs:complexType name="PlayReadyLicenseResponseTemplate">
        <xs:sequence>
          <xs:element name="LicenseTemplates" nillable="true" type="tns:ArrayOfPlayReadyLicenseTemplate" />
          <xs:element minOccurs="0" name="ResponseCustomData" nillable="true" type="xs:string">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
        </xs:sequence>
      </xs:complexType>
      <xs:element name="PlayReadyLicenseResponseTemplate" nillable="true" type="tns:PlayReadyLicenseResponseTemplate" />
      <xs:complexType name="ArrayOfPlayReadyLicenseTemplate">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="unbounded" name="PlayReadyLicenseTemplate" nillable="true" type="tns:PlayReadyLicenseTemplate" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ArrayOfPlayReadyLicenseTemplate" nillable="true" type="tns:ArrayOfPlayReadyLicenseTemplate" />
      <xs:complexType name="PlayReadyLicenseTemplate">
        <xs:sequence>
          <xs:element minOccurs="0" name="AllowTestDevices" type="xs:boolean" />
          <xs:element minOccurs="0" name="BeginDate" nillable="true" type="xs:dateTime">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element name="ContentKey" nillable="true" type="tns:PlayReadyContentKey" />
          <xs:element minOccurs="0" name="ContentType" type="tns:ContentType">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ExpirationDate" nillable="true" type="xs:dateTime">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="GracePeriod" nillable="true" type="ser:duration">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="LicenseType" type="tns:PlayReadyLicenseType" />
          <xs:element minOccurs="0" name="PlayRight" nillable="true" type="tns:PlayReadyPlayRight" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="PlayReadyLicenseTemplate" nillable="true" type="tns:PlayReadyLicenseTemplate" />
      <xs:simpleType name="PlayReadyLicenseType">
        <xs:restriction base="xs:string">
          <xs:enumeration value="Nonpersistent" />
          <xs:enumeration value="Persistent" />
        </xs:restriction>
      </xs:simpleType>
      <xs:element name="PlayReadyLicenseType" nillable="true" type="tns:PlayReadyLicenseType" />
      <xs:complexType name="PlayReadyPlayRight">
        <xs:sequence>
          <xs:element minOccurs="0" name="AgcAndColorStripeRestriction" nillable="true" type="tns:AgcAndColorStripeRestriction">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="AllowPassingVideoContentToUnknownOutput" type="tns:UnknownOutputPassingOption">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="AnalogVideoOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="CompressedDigitalAudioOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="CompressedDigitalVideoOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="DigitalVideoOnlyContentRestriction" type="xs:boolean">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ExplicitAnalogTelevisionOutputRestriction" nillable="true" type="tns:ExplicitAnalogTelevisionRestriction">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="FirstPlayExpiration" nillable="true" type="ser:duration">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ImageConstraintForAnalogComponentVideoRestriction" type="xs:boolean">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ImageConstraintForAnalogComputerMonitorRestriction" type="xs:boolean">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ScmsRestriction" nillable="true" type="tns:ScmsRestriction">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="UncompressedDigitalAudioOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="UncompressedDigitalVideoOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
        </xs:sequence>
      </xs:complexType>
      <xs:element name="PlayReadyPlayRight" nillable="true" type="tns:PlayReadyPlayRight" />
      <xs:simpleType name="UnknownOutputPassingOption">
        <xs:restriction base="xs:string">
          <xs:enumeration value="NotAllowed" />
          <xs:enumeration value="Allowed" />
          <xs:enumeration value="AllowedWithVideoConstriction" />
        </xs:restriction>
      </xs:simpleType>
      <xs:element name="UnknownOutputPassingOption" nillable="true" type="tns:UnknownOutputPassingOption" />
      <xs:complexType name="ScmsRestriction">
        <xs:sequence>
          <xs:element minOccurs="0" name="ConfigurationData" type="xs:unsignedByte" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ScmsRestriction" nillable="true" type="tns:ScmsRestriction" />
    </xs:schema>



## <a name="media-services-learning-paths"></a><span data-ttu-id="03377-152">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="03377-152">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="03377-153">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="03377-153">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

