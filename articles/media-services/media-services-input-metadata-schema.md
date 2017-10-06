---
title: "aaaAzure Media Services 輸入中繼資料結構描述 |Microsoft 文件"
description: "hello 主題提供 Azure Media Services 輸入中繼資料結構描述的概觀。"
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: d72848e2-4b65-4c84-94bc-e2a90a6e7f47
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako
ms.openlocfilehash: 9b72c6ff317aa98451ea75548465dc6023b44a55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="input-metadata"></a>輸入中繼資料
輸入的資產或多個相關聯的編碼工作，是您想 tooperform 部分編碼工作。  完成工作時，就會產生輸出資產。  hello 輸出資產包含視訊、 音訊、 縮圖、 資訊清單，等 hello 輸出資產也包含 hello 輸入資產的相關中繼資料檔案。 hello hello 中繼資料 XML 檔案名稱具有下列格式的 hello: &lt;a&gt;_metadata.xml (例如，41114ad3-eb5e-4c 57-8 d 92-5354e2b7d4a4_metadata.xml)，其中&lt;a&gt;為 hello AssetIdhello 輸入資產的值。  

如果您想 tooexamine hello 中繼資料檔案時，您可以建立**SAS**定位器和下載 hello 檔案 tooyour 本機電腦。 您可以找到範例如何 toocreate SAS 定位器和下載檔案[使用 hello Media Services.NET SDK Extensions](media-services-dotnet-get-started.md)。  

本主題討論 hello 項目和 hello XML 結構描述的類型上的 hello 輸入中繼資料 (&lt;a&gt;_metadata.xml) 為基礎。  如需 hello 檔案，其中包含有關 hello 輸出資產的中繼資料資訊，請參閱[輸出中繼資料](media-services-output-metadata-schema.md)。  

> [!NOTE]
> 您可以找到 hello[結構描述程式碼](media-services-input-metadata-schema.md#code) [XML 範例](media-services-input-metadata-schema.md#xml)hello 本主題結尾處。  
> 
> 

## <a name="AssetFiles"></a> Assetfile 元素 (根元素)
包含集合[AssetFile 元素](media-services-input-metadata-schema.md#AssetFile)s hello 編碼工作。  

請參閱本主題的 hello 結尾 XML 範例： [XML 範例](media-services-input-metadata-schema.md#xml)。  

| 名稱 | 說明 |
| --- | --- |
| **AssetFile**<br /><br /> minOccurs="1" maxOccurs="unbounded" |單一子元素。 如需詳細資訊，請參閱 [AssetFile 元素](media-services-input-metadata-schema.md#AssetFile)。 |

## <a name="AssetFile"></a> AssetFile 元素
 包含可描述資產檔案的屬性和元素。  

 請參閱本主題的 hello 結尾 XML 範例： [XML 範例](media-services-input-metadata-schema.md#xml)。  

### <a name="attributes"></a>屬性
| 名稱 | 類型 | 說明 |
| --- | --- | --- |
| **名稱**<br /><br /> 必要 |**xs:string** |資產檔案名稱。 |
| **大小**<br /><br /> 必要 |**xs:long** |Hello 資產檔案，以位元組為單位的大小。 |
| **Duration**<br /><br /> 必要 |**xs:duration** |內容播放持續時間。 範例：Duration="PT25M37.757S"。 |
| **NumberOfStreams**<br /><br /> 必要 |**xs:int** |Hello 資產檔案中的資料流數目。 |
| **FormatNames**<br /><br /> 必要 |**xs:string** |Format names. |
| **FormatVerboseNames**<br /><br /> 必要 |**xs:string** |格式詳細資訊名稱。 |
| **StartTime** |**xs:duration** |內容開始時間。 範例︰StartTime="PT2.669S"。 |
| **OverallBitRate** |**xs:int** |Hello 資產檔案，以 kbps 為單位的平均位元速率。 |

> [!NOTE]
> hello 下列 4 子元素必須循序出現。  
> 
> 

### <a name="child-elements"></a>子元素
| 名稱 | 類型 | 說明 |
| --- | --- | --- |
| **Programs**<br /><br /> minOccurs="0" | |所有的集合[程式項目](media-services-input-metadata-schema.md#Programs)hello 資產檔案格式為 MPEG-TS 時。 |
| **VideoTracks**<br /><br /> minOccurs="0" | |每個實體資產檔案可以包含零個或多個交錯形成適當容器格式的視訊播放軌。 這個項目包含所有的集合[Videotrack 元素](media-services-input-metadata-schema.md#VideoTracks)hello 資產檔案的一部分。 |
| **AudioTracks**<br /><br /> minOccurs="0" | |每個實體資產檔案可以包含零個或多個交錯形成適當容器格式的音訊播放軌。 這個項目包含所有的集合[Audiotrack 元素](media-services-input-metadata-schema.md#AudioTracks)hello 資產檔案的一部分。 |
| **Metadata**<br /><br /> minOccurs="0" maxOccurs="unbounded" |[MetadataType](media-services-input-metadata-schema.md#MetadataType) |資產檔案的中繼資料 (以索引鍵\值字串表示)。 例如：<br /><br /> **&lt;Metadata key="language" value="eng" /&gt;** |

## <a name="TrackType"></a> TrackType
請參閱本主題的 hello 結尾 XML 範例： [XML 範例](media-services-input-metadata-schema.md#xml)。  

### <a name="attributes"></a>屬性
| 名稱 | 類型 | 說明 |
| --- | --- | --- |
| **Id**<br /><br /> 必要 |**xs:int** |此音訊或視訊播放軌之以零為起始的索引。<br /><br /> 這不一定是該 hello TrackID MP4 檔案中使用。 |
| **Codec** |**xs:string** |視訊播放軌轉碼器字串。 |
| **CodecLongName** |**xs:string** |音訊或視訊播放軌轉碼器長名稱。 |
| **TimeBase**<br /><br /> 必要 |**xs:string** |時間基準。 範例：TimeBase="1/48000" |
| **NumberOfFrames** |**xs:int** |畫面格數 (針對視訊播放軌呈現)。 |
| **StartTime** |**xs:duration** |播放軌開始時間。 範例︰StartTime="PT2.669S" |
| **Duration** |**xs:duration** |播放軌持續時間。 範例：Duration="PTSampleFormat M37.757S"。 |

> [!NOTE]
> hello 下列 2 的子元素必須循序出現。  
> 
> 

### <a name="child-elements"></a>子元素
| 名稱 | 類型 | 說明 |
| --- | --- | --- |
| **Disposition**<br /><br /> minOccurs="0" maxOccurs="1" |[StreamDispositionType](media-services-input-metadata-schema.md#StreamDispositionType) |包含簡報資訊 (例如，特定音訊播放軌是否適用於視障者)。 |
| **Metadata**<br /><br /> minOccurs="0" maxOccurs="unbounded" |[MetadataType](media-services-input-metadata-schema.md#MetadataType) |可以是使用的 toohold 的各種資訊的泛用的索引鍵/值字串。 例如，key=”language” 和 value=”eng”。 |

## <a name="AudioTrackType"></a> AudioTrackType (繼承自 TrackType)
 **AudioTrackType** 是全域複雜類型，其繼承自 [TrackType](media-services-input-metadata-schema.md#TrackType)。  

 hello 類型代表 hello 資產檔案中的特定音訊音軌。  

 請參閱本主題的 hello 結尾 XML 範例： [XML 範例](media-services-input-metadata-schema.md#xml)。  

### <a name="attributes"></a>屬性
| 名稱 | 類型 | 說明 |
| --- | --- | --- |
| **SampleFormat** |**xs:string** |樣本格式。 |
| **ChannelLayout** |**xs:string** |聲道配置。 |
| **Channels**<br /><br /> 必要 |**xs:int** |音訊聲道數目 (0 個或多個)。 |
| **SamplingRate**<br /><br /> 必要 |**xs:int** |音訊取樣率 (每秒或每 Hz 的樣本數)。 |
| **Bitrate** |**xs:int** |音訊平均位元速率，以每秒位元，以從 hello 資產檔案計算而得。 計算 hello 基本資料流裝載，以及這個計數不包含 hello 封裝負荷。 |
| **BitsPerSample** |**xs:int** |位元，每個範例的 hello wFormatTag 格式類型。 |

## <a name="VideoTrackType"></a> VideoTrackType (繼承自 TrackType)
**VideoTrackType** 是全域複雜類型，其繼承自 [TrackType](media-services-input-metadata-schema.md#TrackType)。  

hello 類型代表 hello 資產檔案中的特定視訊音軌。  

請參閱本主題的 hello 結尾 XML 範例： [XML 範例](media-services-input-metadata-schema.md#xml)。  

### <a name="attributes"></a>屬性
| 名稱 | 類型 | 說明 |
| --- | --- | --- |
| **FourCC**<br /><br /> 必要 |**xs:string** |視訊轉碼器 FourCC 代碼。 |
| **設定檔** |**xs:string** |視訊播放軌的設定檔。 |
| **Level** |**xs:string** |視訊播放軌的層級。 |
| **PixelFormat** |**xs:string** |視訊播放軌的像素格式。 |
| **Width**<br /><br /> 必要 |**xs:int** |編碼的視訊寬度 (以像素為單位)。 |
| **Height**<br /><br /> 必要 |**xs:int** |編碼的視訊高度 (以像素為單位)。 |
| **DisplayAspectRatioNumerator**<br /><br /> 必要 |**xs:double** |視訊顯示長寬比的分子。 |
| **DisplayAspectRatioDenominator**<br /><br /> 必要 |**xs:double** |視訊顯示長寬比的分母。 |
| **DisplayAspectRatioDenominator**<br /><br /> 必要 |**xs:double** |視訊樣本長寬比的分子。 |
| **SampleAspectRatioNumerator** |**xs:double** |視訊樣本長寬比的分子。 |
| **SampleAspectRatioNumerator** |**xs:double** |視訊樣本長寬比的分母。 |
| **FrameRate**<br /><br /> 必要 |**xs:decimal** |測量的視訊畫面格速率 (採用 .3f 格式)。 |
| **Bitrate** |**xs:int** |視訊平均位元速率，以 kb / 秒，為從 hello 資產檔案計算而得。 計算 hello 基本資料流裝載，並不包含 hello 封裝負荷。 |
| **MaxGOPBitrate** |**xs:int** |此視訊播放軌的最大 GOP 平均位元速率 (千位元 / 秒)。 |
| **HasBFrames** |**xs:int** |B 畫面格的視訊播放軌數目。 |

## <a name="MetadataType"></a> MetadataType
**MetadataType** 是全域複雜類型，其以索引鍵/值字串的形式描述資產檔案的中繼資料。 例如，key=”language” 和 value=”eng”。  

請參閱本主題的 hello 結尾 XML 範例： [XML 範例](media-services-input-metadata-schema.md#xml)。  

### <a name="attributes"></a>屬性
| 名稱 | 類型 | 說明 |
| --- | --- | --- |
| **key**<br /><br /> 必要 |**xs:string** |hello 索引鍵/值組中的 hello 索引鍵。 |
| **value**<br /><br /> 必要 |**xs:string** |hello 索引鍵/值組中的 hello 值。 |

## <a name="ProgramType"></a> ProgramType
**ProgramType** 是用來描述節目的全域複雜類型。  

### <a name="attributes"></a>屬性
| 名稱 | 類型 | 說明 |
| --- | --- | --- |
| **ProgramId**<br /><br /> 必要 |**xs:int** |Program Id |
| **NumberOfPrograms**<br /><br /> 必要 |**xs:int** |節目數量。 |
| **PmtPid**<br /><br /> 必要 |**xs:int** |節目對應表 (PMT) 包含節目相關資訊。  如需詳細資訊，請參閱 [PMt](http://en.wikipedia.org/wiki/MPEG_transport_stream#PMT)。 |
| **PcrPid**<br /><br /> 必要 |**xs:int** |由解碼器使用。 如需詳細資訊，請參閱 [PCR](http://en.wikipedia.org/wiki/MPEG_transport_stream#PCR) |
| **StartPTS** |**xs: long** |啟動簡報時間戳記。 |
| **EndPTS** |**xs: long** |結束簡報時間戳記。 |

## <a name="StreamDispositionType"></a> StreamDispositionType
**StreamDispositionType**是描述 hello 資料流的全域複雜類型。  

請參閱本主題的 hello 結尾 XML 範例： [XML 範例](media-services-input-metadata-schema.md#xml)。  

### <a name="attributes"></a>屬性
| 名稱 | 類型 | 說明 |
| --- | --- | --- |
| **預設值**<br /><br /> 必要 |**xs:int** |設定這是此屬性 too1 tooindicate hello 預設呈現方式。 |
| **Dub**<br /><br /> 必要 |**xs:int** |設定此屬性 too1 tooindicate hello 名簡報。 |
| **Original**<br /><br /> 必要 |**xs:int** |設定這是此屬性 too1 tooindicate hello 原始簡報。 |
| **Comment**<br /><br /> 必要 |**xs:int** |設定此屬性 too1 tooindicate 此音軌包含評論。 |
| **Lyrics**<br /><br /> 必要 |**xs:int** |設定此屬性 too1 tooindicate 此音軌包含歌詞。 |
| **Karaoke**<br /><br /> 必要 |**xs:int** |設定此屬性 too1 tooindicate 這代表 hello 伴唱帶音軌 （背景音樂、 無人聲）。 |
| **Forced**<br /><br /> 必要 |**xs:int** |設定此屬性 too1 tooindicate，這是強制的 hello 簡報。 |
| **HearingImpaired**<br /><br /> 必要 |**xs:int** |設定此屬性 too1 tooindicate 此音軌適用於 hello 聽覺障礙者。 |
| **VisualImpaired**<br /><br /> 必要 |**xs:int** |設定此屬性 too1 tooindicate 此音軌適用於視覺障礙者 hello。 |
| **CleanEffects**<br /><br /> 必要 |**xs:int** |設定此屬性 too1 tooindicate 此音軌有全新效果。 |
| **AttachedPic**<br /><br /> 必要 |**xs:int** |設定此屬性 too1 tooindicate 此音軌有圖片。 |

## <a name="Programs"></a> Programs 元素
保有多個 **Program** 元素的包裝函式元素。  

### <a name="child-elements"></a>子元素
| 名稱 | 類型 | 說明 |
| --- | --- | --- |
| **Program**<br /><br /> minOccurs="0" maxOccurs="unbounded" |[ProgramType](media-services-input-metadata-schema.md#ProgramType) |為 MPEG-TS 格式的資產檔案，包含 hello 資產檔案中程式的相關資訊。 |

## <a name="VideoTracks"></a> VideoTracks 元素
 保有多個 **VideoTrack** 元素的包裝函式元素。  

 請參閱本主題的 hello 結尾 XML 範例： [XML 範例](media-services-input-metadata-schema.md#xml)。  

### <a name="child-elements"></a>子元素
| 名稱 | 類型 | 說明 |
| --- | --- | --- |
| **VideoTrack**<br /><br /> minOccurs="0" maxOccurs="unbounded" |[VideoTrackType (繼承自 TrackType)](media-services-input-metadata-schema.md#VideoTrackType) |包含 hello 資產檔案中的視訊音軌的相關資訊。 |

## <a name="AudioTracks"></a> AudioTracks 元素
 保有多個 **AudioTrack** 元素的包裝函式元素。  

 請參閱本主題的 hello 結尾 XML 範例： [XML 範例](media-services-input-metadata-schema.md#xml)。  

### <a name="elements"></a>元素
| 名稱 | 類型 | 說明 |
| --- | --- | --- |
| **AudioTrack**<br /><br /> minOccurs="0" maxOccurs="unbounded" |[AudioTrackType (繼承自 TrackType)](media-services-input-metadata-schema.md#AudioTrackType) |包含 hello 資產檔案中的音訊音軌的相關資訊。 |

## <a name="code"></a> 結構描述程式碼
    <?xml version="1.0" encoding="utf-8"?>  
    <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:msdata="urn:schemas-microsoft-com:xml-msdata" version="1.0"  
               xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata"  
               targetNamespace="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata"  
               elementFormDefault="qualified">  

      <xs:complexType name="MetadataType">  
        <xs:attribute name="key"   type="xs:string" use="required"/>  
        <xs:attribute name="value" type="xs:string" use="required"/>  
      </xs:complexType>  

      <xs:complexType name="ProgramType">  
        <xs:attribute name="ProgramId" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>Program Id</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="NumberOfPrograms" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>Number of programs</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="PmtPid" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>pmt pid</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="PcrPid" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>pcr pid</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="StartPTS" type="xs:long">  
          <xs:annotation>  
            <xs:documentation>start pts</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="EndPTS" type="xs:long">  
          <xs:annotation>  
            <xs:documentation>end pts</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
      </xs:complexType>  

      <xs:complexType name="StreamDispositionType">  
        <xs:attribute name="Default"          type="xs:int" use="required" />  
        <xs:attribute name="Dub"              type="xs:int" use="required" />  
        <xs:attribute name="Original"         type="xs:int" use="required" />  
        <xs:attribute name="Comment"          type="xs:int" use="required" />  
        <xs:attribute name="Lyrics"           type="xs:int" use="required" />  
        <xs:attribute name="Karaoke"          type="xs:int" use="required" />  
        <xs:attribute name="Forced"           type="xs:int" use="required" />  
        <xs:attribute name="HearingImpaired"  type="xs:int" use="required" />  
        <xs:attribute name="VisualImpaired"   type="xs:int" use="required" />  
        <xs:attribute name="CleanEffects"     type="xs:int" use="required" />  
        <xs:attribute name="AttachedPic"      type="xs:int" use="required" />  
      </xs:complexType>  

      <xs:complexType name="TrackType" abstract="true">  
        <xs:sequence>  
          <xs:element name="Disposition" type="StreamDispositionType" minOccurs="0" maxOccurs="1"/>  
          <xs:element name="Metadata" type="MetadataType" minOccurs="0" maxOccurs="unbounded"/>  
        </xs:sequence>  
        <xs:attribute name="Id" use="required">  
          <xs:annotation>  
            <xs:documentation>zero-based index of this video track. Note: this is not necessarily hello TrackID as used in an MP4 file</xs:documentation>  
          </xs:annotation>  
          <xs:simpleType>  
            <xs:restriction base="xs:int">  
              <xs:minInclusive value="0"/>  
            </xs:restriction>  
          </xs:simpleType>  
        </xs:attribute>  
        <xs:attribute name="Codec" type="xs:string">  
          <xs:annotation>  
            <xs:documentation>video track codec string</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="CodecLongName" type="xs:string">  
          <xs:annotation>  
            <xs:documentation>video track codec long name</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="TimeBase"  type="xs:string" use="required">  
          <xs:annotation>  
            <xs:documentation>Time base. Example: TimeBase="1/48000"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="NumberOfFrames">  
          <xs:annotation>  
            <xs:documentation>number of frames</xs:documentation>  
          </xs:annotation>  
          <xs:simpleType>  
            <xs:restriction base="xs:int">  
              <xs:minInclusive value="0"/>  
            </xs:restriction>  
          </xs:simpleType>  
        </xs:attribute>  
        <xs:attribute name="StartTime" type="xs:duration">  
          <xs:annotation>  
            <xs:documentation>Track start time. Example: StartTime="PT2.669S"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="Duration" type="xs:duration">  
          <xs:annotation>  
            <xs:documentation>Track duration. Example: Duration="PT25M37.757S"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
      </xs:complexType>  

      <xs:complexType name="VideoTrackType">  
        <xs:annotation>  
          <xs:documentation>A specific video track in hello parent AssetFile</xs:documentation>  
        </xs:annotation>  
        <xs:complexContent>  
          <xs:extension base="TrackType">  
            <xs:attribute name="FourCC" type="xs:string" use="required">  
              <xs:annotation>  
                <xs:documentation>video codec FourCC code</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Profile" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>profile</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Level" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>level</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="PixelFormat" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>Video track's pixel format</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Width" use="required">  
              <xs:annotation>  
                <xs:documentation>encoded video width in pixels</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="Height" use="required">  
              <xs:annotation>  
                <xs:documentation>encoded video height in pixels</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="DisplayAspectRatioNumerator" use="required">  
              <xs:annotation>  
                <xs:documentation>video display aspect ratio numerator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="DisplayAspectRatioDenominator" use="required">  
              <xs:annotation>  
                <xs:documentation>video display aspect ratio denominator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="SampleAspectRatioNumerator">  
              <xs:annotation>  
                <xs:documentation>video sample aspect ratio numerator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="SampleAspectRatioDenominator">  
              <xs:annotation>  
                <xs:documentation>video sample aspect ratio denominator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="FrameRate" use="required">  
              <xs:annotation>  
                <xs:documentation>measured video frame rate in .3f format</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:decimal">  
                  <xs:minInclusive value="0"/>  
                  <xs:fractionDigits value="3"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="Bitrate">  
              <xs:annotation>  
                <xs:documentation>average video bit rate in kilobits per second, as calculated from hello AssetFile. Counts only hello elementary stream payload, and does not include hello packaging overhead</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="MaxGOPBitrate">  
              <xs:annotation>  
                <xs:documentation>Max GOP average bitrate for this video track, in kilobits per second</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="HasBFrames" type="xs:int">  
              <xs:annotation>  
                <xs:documentation>video track number of B frames</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
          </xs:extension>  
        </xs:complexContent>  
      </xs:complexType>  

      <xs:complexType name="AudioTrackType">  
        <xs:annotation>  
          <xs:documentation>a specific audio track in hello parent AssetFile</xs:documentation>  
        </xs:annotation>  
        <xs:complexContent>  
          <xs:extension base="TrackType">  
            <xs:attribute name="SampleFormat"  type="xs:string">  
              <xs:annotation>  
                <xs:documentation>sample format</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="ChannelLayout"  type="xs:string">  
              <xs:annotation>  
                <xs:documentation>channel layout</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Channels" use="required">  
              <xs:annotation>  
                <xs:documentation>number of audio channels</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="SamplingRate" use="required">  
              <xs:annotation>  
                <xs:documentation>audio sampling rate in samples/sec or Hz</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="Bitrate">  
              <xs:annotation>  
                <xs:documentation>average audio bit rate in bits per second, as calculated from hello AssetFile. Counts only hello elementary stream payload, and does not include hello packaging overhead</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="BitsPerSample">  
              <xs:annotation>  
                <xs:documentation>Bits per sample for hello wFormatTag format type</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
          </xs:extension>  
        </xs:complexContent>  
      </xs:complexType>  

      <xs:element name="AssetFiles">  
        <xs:annotation>  
          <xs:documentation>Collection of AssetFile entries for hello encoding job</xs:documentation>  
        </xs:annotation>  
        <xs:complexType>  
          <xs:sequence>  
            <xs:element name="AssetFile" minOccurs="1" maxOccurs="unbounded">  
              <xs:annotation>  
                <xs:documentation>asset file</xs:documentation>  
              </xs:annotation>  
              <xs:complexType>  
                <xs:sequence>  
                  <xs:element name="Programs" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>This is hello collection of all programs when file is MPEG-TS</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="Program" type="ProgramType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="VideoTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format. This is hello collection of all those video tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="VideoTrack" type="VideoTrackType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="AudioTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format. This is hello collection of all those audio tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="AudioTrack" type="AudioTrackType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="Metadata" type="MetadataType" minOccurs="0" maxOccurs="unbounded" />  
                </xs:sequence>  
                <xs:attribute name="Name" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>hello media asset file name</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="Size" use="required">  
                  <xs:annotation>  
                    <xs:documentation>size of file in bytes</xs:documentation>  
                  </xs:annotation>  
                  <xs:simpleType>  
                    <xs:restriction base="xs:long">  
                      <xs:minInclusive value="0"/>  
                    </xs:restriction>  
                  </xs:simpleType>  
                </xs:attribute>  
                <xs:attribute name="Duration" type="xs:duration" use="required">  
                  <xs:annotation>  
                    <xs:documentation>content play back duration. Example: Duration="PT25M37.757S"</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="NumberOfStreams" type="xs:int" use="required">  
                  <xs:annotation>  
                    <xs:documentation>number of streams in asset file</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="FormatNames" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>format names</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="FormatVerboseName" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>format verbose names</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="StartTime" type="xs:duration">  
                  <xs:annotation>  
                    <xs:documentation>content start time. Example: StartTime="PT2.669S"</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="OverallBitRate">  
                  <xs:annotation>  
                    <xs:documentation>average bitrate of hello asset file in kbps</xs:documentation>  
                  </xs:annotation>  
                  <xs:simpleType>  
                    <xs:restriction base="xs:int">  
                      <xs:minInclusive value="0"/>  
                    </xs:restriction>  
                  </xs:simpleType>  
                </xs:attribute>  
              </xs:complexType>  
            </xs:element>  
          </xs:sequence>  
        </xs:complexType>  
      </xs:element>  
    </xs:schema>  


## <a name="xml"></a> XML 範例
hello 以下是 hello 輸入中繼資料檔案的範例。  

    <?xml version="1.0" encoding="utf-8"?>  
    <AssetFiles xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata">  
      <AssetFile Name="bear.mp4" Size="1973733" Duration="PT12.678S" NumberOfStreams="2" FormatNames="mov,mp4,m4a,3gp,3g2,mj2" FormatVerboseName="QuickTime / MOV" StartTime="PT0S" OverallBitRate="1245">  
        <VideoTracks>  
          <VideoTrack Id="1" Codec="h264" CodecLongName="H.264 / AVC / MPEG-4 AVC / MPEG-4 part 10" TimeBase="1/29970" NumberOfFrames="375" StartTime="PT0.034S" Duration="PT12.645S" FourCC="avc1" Profile="High" Level="4.1" PixelFormat="yuv420p" Width="512" Height="384" DisplayAspectRatioNumerator="4" DisplayAspectRatioDenominator="3" SampleAspectRatioNumerator="1" SampleAspectRatioDenominator="1" FrameRate="29.656" Bitrate="1043" HasBFrames="1">  
            <Disposition Default="1" Dub="0" Original="0" Comment="0" Lyrics="0" Karaoke="0" Forced="0" HearingImpaired="0" VisualImpaired="0" CleanEffects="0" AttachedPic="0" />  
            <Metadata key="creation_time" value="2010-03-10 16:11:56" />  
            <Metadata key="language" value="eng" />  
            <Metadata key="handler_name" value="Mainconcept MP4 Video Media Handler" />  
          </VideoTrack>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="aac" CodecLongName="AAC (Advanced Audio Coding)" TimeBase="1/44100" NumberOfFrames="546" StartTime="PT0S" Duration="PT12.678S" SampleFormat="fltp" ChannelLayout="stereo" Channels="2" SamplingRate="44100" Bitrate="156" BitsPerSample="0">  
            <Disposition Default="1" Dub="0" Original="0" Comment="0" Lyrics="0" Karaoke="0" Forced="0" HearingImpaired="0" VisualImpaired="0" CleanEffects="0" AttachedPic="0" />  
            <Metadata key="creation_time" value="2010-03-10 16:11:56" />  
            <Metadata key="language" value="eng" />  
            <Metadata key="handler_name" value="Mainconcept MP4 Sound Media Handler" />  
          </AudioTrack>  
        </AudioTracks>  
        <Metadata key="major_brand" value="mp42" />  
        <Metadata key="minor_version" value="0" />  
        <Metadata key="compatible_brands" value="mp42mp41" />  
        <Metadata key="creation_time" value="2010-03-10 16:11:53" />  
        <Metadata key="comment" value="Courtesy of National Geographic.  Used by Permission." />  
      </AssetFile>  
    </AssetFiles>  

## <a name="next-steps"></a>後續步驟
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

