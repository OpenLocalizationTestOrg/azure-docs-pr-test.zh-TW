---
title: "aaaMedia Services PlayReady 授權範本概觀"
description: "本主題提供使用 tooconfigure PlayReady 授權的 PlayReady 授權範本的概觀。"
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
ms.openlocfilehash: 5a5ba930c56f70038db204681486ebc4308199fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="media-services-playready-license-template-overview"></a><span data-ttu-id="44ff3-103">媒體服務 PlayReady 授權範本概觀</span><span class="sxs-lookup"><span data-stu-id="44ff3-103">Media Services PlayReady license template overview</span></span>
<span data-ttu-id="44ff3-104">Azure 媒體服務現在提供一種服務，來傳遞 Microsoft PlayReady 授權。</span><span class="sxs-lookup"><span data-stu-id="44ff3-104">Azure Media Services now provides a service for delivering Microsoft PlayReady licenses.</span></span> <span data-ttu-id="44ff3-105">Hello 使用者播放程式 (例如，Silverlight) 嘗試 tooplay 時受 PlayReady 保護的內容，將要求傳送的 toohello 授權傳遞服務 tooobtain 授權。</span><span class="sxs-lookup"><span data-stu-id="44ff3-105">When hello end user player (for example, Silverlight) tries tooplay your PlayReady protected content, a request is sent toohello license delivery service tooobtain a license.</span></span> <span data-ttu-id="44ff3-106">如果 hello 授權服務核准 hello 要求，就會發出這是傳送的 toohello 用戶端 hello 授權，而且可以是使用的 toodecrypt 插 hello 指定的內容。</span><span class="sxs-lookup"><span data-stu-id="44ff3-106">If hello license service approves hello request, it issues hello license which is sent toohello client and can be used toodecrypt and play hello specified content.</span></span>

<span data-ttu-id="44ff3-107">媒體服務也會提供可讓您設定 PlayReady 授權的 API。</span><span class="sxs-lookup"><span data-stu-id="44ff3-107">Media Services also provides APIs that let you configure your PlayReady licenses.</span></span> <span data-ttu-id="44ff3-108">授權包含 hello 權限和限制您想要 hello PlayReady DRM 執行階段 tooenforce 當使用者想 tooplayback 受保護的內容。</span><span class="sxs-lookup"><span data-stu-id="44ff3-108">Licenses contain hello rights and restrictions that you want for hello PlayReady DRM runtime tooenforce when a user is trying tooplayback protected content.</span></span>
<span data-ttu-id="44ff3-109">以下是您可以指定之 PlayReady 授權限制的一些範例：</span><span class="sxs-lookup"><span data-stu-id="44ff3-109">Below are some examples of PlayReady license restrictions that you can specify:</span></span>

* <span data-ttu-id="44ff3-110">hello 從哪些 hello 授權開始生效的日期時間。</span><span class="sxs-lookup"><span data-stu-id="44ff3-110">hello DateTime from which hello license is valid.</span></span>
* <span data-ttu-id="44ff3-111">hello hello 授權到期時的日期時間值。</span><span class="sxs-lookup"><span data-stu-id="44ff3-111">hello DateTime value when hello license expires.</span></span> 
* <span data-ttu-id="44ff3-112">針對儲存在永續性儲存體上 hello 用戶端 hello 授權 toobe。</span><span class="sxs-lookup"><span data-stu-id="44ff3-112">For hello license toobe saved in persistent storage on hello client.</span></span> <span data-ttu-id="44ff3-113">持續性授權是常用的 tooallow 離線播放 hello 內容。</span><span class="sxs-lookup"><span data-stu-id="44ff3-113">Persistent licenses are typically used tooallow offline playback of hello content.</span></span>
* <span data-ttu-id="44ff3-114">hello 最低安全性層級，播放程式必須要有 tooplay 您的內容。</span><span class="sxs-lookup"><span data-stu-id="44ff3-114">hello minimum security level that a player must have tooplay your content.</span></span> 
* <span data-ttu-id="44ff3-115">hello 輸出音訊/視訊內容的 hello 輸出控制項的保護層級。</span><span class="sxs-lookup"><span data-stu-id="44ff3-115">hello output protection level for hello output controls for audio\video content.</span></span> 
* <span data-ttu-id="44ff3-116">如需詳細資訊，請參閱下一節 (3.5) 中的 hello hello 輸出控制項[PlayReady 相容性規則](https://www.microsoft.com/playready/licensing/compliance/)文件。</span><span class="sxs-lookup"><span data-stu-id="44ff3-116">For more information, see hello Output Controls section (3.5) in hello [PlayReady Compliance Rules](https://www.microsoft.com/playready/licensing/compliance/) document.</span></span>

> [!NOTE]
> <span data-ttu-id="44ff3-117">目前，您可以只設定 hello （此為必要權限） 的 hello PlayReady 授權的 PlayRight。</span><span class="sxs-lookup"><span data-stu-id="44ff3-117">Currently, you can only configure hello PlayRight of hello PlayReady license (this right is required).</span></span> <span data-ttu-id="44ff3-118">hello PlayRight 讓 hello 用戶端 hello 能力 tooplayback hello 內容。</span><span class="sxs-lookup"><span data-stu-id="44ff3-118">hello PlayRight gives hello client hello ability tooplayback hello content.</span></span> <span data-ttu-id="44ff3-119">hello PlayRight 也可讓設定限制特定 tooplayback。</span><span class="sxs-lookup"><span data-stu-id="44ff3-119">hello PlayRight also allows configuring restrictions specific tooplayback.</span></span> <span data-ttu-id="44ff3-120">如需詳細資訊，請參閱 [PlayReadyPlayRight](media-services-playready-license-template-overview.md#PlayReadyPlayRight)。</span><span class="sxs-lookup"><span data-stu-id="44ff3-120">For more information, see [PlayReadyPlayRight](media-services-playready-license-template-overview.md#PlayReadyPlayRight).</span></span>
> 
> 

<span data-ttu-id="44ff3-121">使用 Media Services tooconfigure PlayReady 授權，您必須設定 hello Media Services PlayReady 授權範本。</span><span class="sxs-lookup"><span data-stu-id="44ff3-121">tooconfigure PlayReady licenses using Media Services, you must configure hello Media Services PlayReady license template.</span></span> <span data-ttu-id="44ff3-122">hello 範本是以 XML 定義。</span><span class="sxs-lookup"><span data-stu-id="44ff3-122">hello template is defined in XML.</span></span>

<span data-ttu-id="44ff3-123">hello 下列範例會設定基本串流授權的 hello 最簡單的 （且最常見的） 範本。</span><span class="sxs-lookup"><span data-stu-id="44ff3-123">hello following example shows hello simplest (and most common) template that configures a basic streaming license.</span></span> <span data-ttu-id="44ff3-124">與此授權，您的用戶端會無法 tooplayback PlayReady 受保護的內容。</span><span class="sxs-lookup"><span data-stu-id="44ff3-124">With this license, your clients would be able tooplayback your PlayReady protected content.</span></span>

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

<span data-ttu-id="44ff3-125">hello XML 符合 toohello PlayReady 授權範本 XML 結構描述 hello PlayReady 授權範本 XML 結構描述 > 一節中所定義。</span><span class="sxs-lookup"><span data-stu-id="44ff3-125">hello XML conforms toohello PlayReady license template XML schema defined in hello PlayReady license template XML schema section.</span></span>

<span data-ttu-id="44ff3-126">Media Services 也會定義一組可能是使用的 tooserialized 與已還原序列化的 tooand 從 hello XML 的.NET 類別。</span><span class="sxs-lookup"><span data-stu-id="44ff3-126">Media Services also defines a set of .NET classes that could be used tooserialized and deserialized tooand from hello XML.</span></span> <span data-ttu-id="44ff3-127">對於主要類別的描述，請參閱 [媒體服務 .NET 類別](media-services-playready-license-template-overview.md#classes)。</span><span class="sxs-lookup"><span data-stu-id="44ff3-127">For description of main classes, see [Media Services .NET classes](media-services-playready-license-template-overview.md#classes).</span></span> <span data-ttu-id="44ff3-128">所使用的 tooconfigure 授權範本。</span><span class="sxs-lookup"><span data-stu-id="44ff3-128">that are used tooconfigure license templates.</span></span>

<span data-ttu-id="44ff3-129">如需使用.NET 的端對端範例類別 tooconfigure hello PlayReady 授權範本，請參閱[使用 PlayReady 動態加密和授權傳遞服務](media-services-protect-with-drm.md)。</span><span class="sxs-lookup"><span data-stu-id="44ff3-129">For an end-to-end example that uses .NET classes tooconfigure hello PlayReady license template, see [Using PlayReady Dynamic Encryption and License Delivery Service](media-services-protect-with-drm.md).</span></span>

## <span data-ttu-id="44ff3-130"><a id="classes"></a>會使用的 tooconfigure 授權範本的 Media Services.NET 類別</span><span class="sxs-lookup"><span data-stu-id="44ff3-130"><a id="classes"></a>Media Services .NET classes that are used tooconfigure license templates</span></span>
<span data-ttu-id="44ff3-131">hello 下面是 hello 主要.NET 類別會使用的 tooconfigure Media Services PlayReady 授權範本。</span><span class="sxs-lookup"><span data-stu-id="44ff3-131">hello following are hello main .NET classes are used tooconfigure Media Services PlayReady license templates.</span></span> <span data-ttu-id="44ff3-132">這些類別對應 toohello 中定義的型別[PlayReady 授權範本 XML 結構描述](media-services-playready-license-template-overview.md#schema)。</span><span class="sxs-lookup"><span data-stu-id="44ff3-132">These classes map toohello types defined in [PlayReady license template XML schema](media-services-playready-license-template-overview.md#schema).</span></span>

<span data-ttu-id="44ff3-133">hello [MediaServicesLicenseTemplateSerializer](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.mediaserviceslicensetemplateserializer.aspx)類別是使用的 tooserialize 而且 tooand 從 hello Media Services 授權範本 XML 還原序列化。</span><span class="sxs-lookup"><span data-stu-id="44ff3-133">hello [MediaServicesLicenseTemplateSerializer](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.mediaserviceslicensetemplateserializer.aspx) class is used tooserialize and deserialize tooand from hello Media Services license template XML.</span></span>

### <a name="playreadylicenseresponsetemplate"></a><span data-ttu-id="44ff3-134">PlayReadyLicenseResponseTemplate</span><span class="sxs-lookup"><span data-stu-id="44ff3-134">PlayReadyLicenseResponseTemplate</span></span>
<span data-ttu-id="44ff3-135">[PlayReadyLicenseResponseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicenseresponsetemplate.aspx) -這個類別代表傳送後 toohello 終端使用者 hello 回應 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="44ff3-135">[PlayReadyLicenseResponseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicenseresponsetemplate.aspx) - This class represents hello template for hello response sent back toohello end user.</span></span> <span data-ttu-id="44ff3-136">它包含的欄位，自訂資料之間的字串 hello 授權伺服器 hello 應用程式 （可能是適用於自訂應用程式邏輯） 以及一或多個授權範本的清單。</span><span class="sxs-lookup"><span data-stu-id="44ff3-136">It contains a field for a custom data string between hello license server and hello application (may be useful for custom app logic) as well as a list of one or more license templates.</span></span>

<span data-ttu-id="44ff3-137">這是 hello hello 範本階層中的 「 最上層 」 類別。</span><span class="sxs-lookup"><span data-stu-id="44ff3-137">This is hello “top level” class in hello template hierarchy.</span></span> <span data-ttu-id="44ff3-138">表示 hello 回應範本包含授權範本的清單，然後 hello 授權範本則包含 （直接或間接） 的所有 hello 組成 hello 範本資料 toobe 序列化其他類別。</span><span class="sxs-lookup"><span data-stu-id="44ff3-138">Meaning that hello response template includes a list of license templates and hello license templates include (directly or indirectly) all of hello other classes that make up hello template data toobe serialized.</span></span>

### <a name="playreadylicensetemplate"></a><span data-ttu-id="44ff3-139">PlayReadyLicenseTemplate</span><span class="sxs-lookup"><span data-stu-id="44ff3-139">PlayReadyLicenseTemplate</span></span>
<span data-ttu-id="44ff3-140">[PlayReadyLicenseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicensetemplate.aspx) -hello 類別代表用於建立 PlayReady 授權 toobe 傳回 toohello 終端使用者的授權範本。</span><span class="sxs-lookup"><span data-stu-id="44ff3-140">[PlayReadyLicenseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicensetemplate.aspx) - hello class represents a license template for creating PlayReady licenses toobe returned toohello end users.</span></span> <span data-ttu-id="44ff3-141">它包含 hello hello hello 授權中的內容金鑰資料，任何權限或限制 toobe 由執行 hello PlayReady DRM 執行階段時使用 hello 內容金鑰。</span><span class="sxs-lookup"><span data-stu-id="44ff3-141">It contains hello data on hello content key in hello license and any rights or restrictions toobe enforced by hello PlayReady DRM runtime when using hello content key.</span></span>

### <span data-ttu-id="44ff3-142"><a id="PlayReadyPlayRight"></a>PlayReadyPlayRight</span><span class="sxs-lookup"><span data-stu-id="44ff3-142"><a id="PlayReadyPlayRight"></a>PlayReadyPlayRight</span></span>
<span data-ttu-id="44ff3-143">[PlayReadyPlayRight](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadyplayright.aspx) -此類別代表 PlayReady 授權的 PlayRight hello。</span><span class="sxs-lookup"><span data-stu-id="44ff3-143">[PlayReadyPlayRight](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadyplayright.aspx) - This class represents hello PlayRight of a PlayReady license.</span></span> <span data-ttu-id="44ff3-144">它會授與 hello 使用者 hello 能力 tooplayback，hello 內容主旨 toohello 零或更多限制設定在 hello 授權之下，而且在 hello （針對播放特定原則） PlayRight 本身。</span><span class="sxs-lookup"><span data-stu-id="44ff3-144">It grants hello user hello ability tooplayback hello content subject toohello zero or more restrictions configured in hello license and on hello PlayRight itself (for playback specific policy).</span></span> <span data-ttu-id="44ff3-145">大部分的 hello PlayRight hello 原則有 toodo 輸出限制，以控制可播放 hello 內容的輸出中的 hello 類型與任何必須要備妥使用給定的輸出時的限制。</span><span class="sxs-lookup"><span data-stu-id="44ff3-145">Much of hello policy on hello PlayRight has toodo with output restrictions which control hello types of outputs that hello content can be played over and any restrictions that must be put in place when using a given output.</span></span> <span data-ttu-id="44ff3-146">例如，如果啟用 DigitalVideoOnlyContentRestriction，hello 然後 hello DRM 執行階段將只會允許 hello 視訊 toobe 透過數位輸出 （類比視訊輸出不被允許 toopass hello 內容）。</span><span class="sxs-lookup"><span data-stu-id="44ff3-146">For example, if hello DigitalVideoOnlyContentRestriction is enabled, then hello DRM runtime will only allow hello video toobe displayed over digital outputs (analog video outputs won’t be allowed toopass hello content).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="44ff3-147">這些類型的限制可能非常強大，但也會影響 hello 經驗。</span><span class="sxs-lookup"><span data-stu-id="44ff3-147">These types of restrictions can be very powerful but can also affect hello consumer experience.</span></span> <span data-ttu-id="44ff3-148">如果 hello 輸出保護設定過於嚴格，hello 內容可能無法播放某些用戶端上。</span><span class="sxs-lookup"><span data-stu-id="44ff3-148">If hello output protections are configured too restrictive, hello content might be unplayable on some clients.</span></span> <span data-ttu-id="44ff3-149">如需詳細資訊，請參閱 hello [PlayReady 相容性規則](https://www.microsoft.com/playready/licensing/compliance/)文件。</span><span class="sxs-lookup"><span data-stu-id="44ff3-149">For more information, see hello [PlayReady Compliance Rules](https://www.microsoft.com/playready/licensing/compliance/) document.</span></span>
> 
> 

<span data-ttu-id="44ff3-150">如需 Silverlight 支援的保護層級的範例，請參閱： [Silverlight 支援輸出保護](http://go.microsoft.com/fwlink/?LinkId=617318)。</span><span class="sxs-lookup"><span data-stu-id="44ff3-150">For an example of what protection levels Silverlight supports, see: [Silverlight support for output protections](http://go.microsoft.com/fwlink/?LinkId=617318).</span></span>

## <span data-ttu-id="44ff3-151"><a id="schema"></a>PlayReady 授權範本 XML 結構描述</span><span class="sxs-lookup"><span data-stu-id="44ff3-151"><a id="schema"></a>PlayReady license template XML schema</span></span>
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



## <a name="media-services-learning-paths"></a><span data-ttu-id="44ff3-152">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="44ff3-152">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="44ff3-153">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="44ff3-153">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

