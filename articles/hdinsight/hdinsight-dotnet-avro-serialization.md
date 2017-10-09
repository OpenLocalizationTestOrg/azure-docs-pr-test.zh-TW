---
title: "Hadoop-Microsoft Avro Library-Azure 中的 aaaSerialize 資料 |Microsoft 文件"
description: "深入了解如何 tooserialize 和還原序列化使用 hello Microsoft Avro Library toopersist toomemory、 資料庫或檔案的 HDInsight 上的 Hadoop 中的資料。"
keywords: avro, hadoop avro
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: c78dc20d-5d8d-4366-94ac-abbe89aaac58
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: jgao
ms.custom: hdiseo17may2017
ms.openlocfilehash: f364f8e855a54c0fc160e9a106ec8d5b30c6db23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="serialize-data-in-hadoop-with-hello-microsoft-avro-library"></a>序列化 Hadoop 中的資料與 hello Microsoft Avro Library

>[!NOTE]
>microsoft 不再支援 hello Avro SDK。 支援的開放原始碼社群 hello 程式庫。 hello 程式庫的 hello 來源位於[Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro)。

本主題說明如何 toouse hello [Microsoft Avro Library](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro) tooserialize 物件與其他資料結構到資料流 toopersist 它們 toomemory、 資料庫或檔案。 它也會示範如何 toodeserialize 它們 toorecover hello 原始物件。

[!INCLUDE [windows-only](../../includes/hdinsight-windows-only.md)]

## <a name="apache-avro"></a>Apache Avro
hello <a href="https://hadoopsdk.codeplex.com/wikipage?title=Avro%20Library" target="_blank">Microsoft Avro Library</a>實作 hello hello Microsoft.NET 環境 Apache Avro 資料序列化系統。 Apache Avro 提供一個可用於序列化的壓縮二進位資料交換格式。 它會使用<a href="http://www.json.org" target="_blank">JSON</a> toodefine underwrites 語言互通性語言無從驗證結構描述。 以某個語言序列化的資料可以使用另一個語言讀取。 目前支援 C、C++、C#、Java、PHP、Python 和 Ruby。 Hello 格式的詳細的資訊位於 hello <a href="http://avro.apache.org/docs/current/spec.html" target="_blank">Apache Avro 規格</a>。 

>[!NOTE]
>hello Microsoft Avro Library 不支援此規格的 hello 遠端程序呼叫 (Rpc) 的一部分。
>

hello 序列化表示 hello Avro 系統中的物件會包含兩個部分： 結構描述和實際值。 hello Avro 結構描述會描述 hello 的 hello 序列化 JSON 資料的語言無關的資料模型。 它會與資料的二進位表示並存。 具有 hello 分開 hello 二進位表示法的結構描述允許使用沒有每個值的額外費用，讓序列化快速、 以及 hello 表示小撰寫每個物件 toobe。

## <a name="hello-hadoop-scenario"></a>hello Hadoop 案例
Azure HDInsight 和其他 Apache Hadoop 的環境中廣泛使用 hello Apache Avro 序列化格式。 Avro 提供便利的方式 toorepresent Hadoop MapReduce 工作內的複雜資料結構。 hello 格式 Avro 檔案 （Avro 物件容器檔案） 的已設計的 toosupport hello 分散式 MapReduce 程式撰寫模型。 hello 啟用 hello 散發的重要功能是 「 可分割的圖形 「 hello 任一個可搜尋檔案中的任何點和從特定的區塊開始讀取 hello 檔案。

## <a name="serialization-in-avro-library"></a>Avro Library 中的序列化
hello Avro.NET 程式庫支援序列化物件的兩種的方式：

* **反映**-hello hello 類型的 JSON 結構描述會自動建置 hello 資料中的 hello.NET 型別 toobe 序列化合約屬性。
* **泛型記錄**-由 hello 記錄中明確指定 JSON 結構描述[ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx)類別沒有.NET 型別時存在 hello 資料 toobe 的 toodescribe hello 結構描述序列化。

當 tooboth hello 寫入器 」 和 「 hello 資料流的讀取器知道 hello 資料結構描述時，可以傳送 hello 資料，不會其結構描述。 在案例中使用 Avro 物件容器檔案時，hello 結構描述儲存在 hello 檔案。 可以指定其他參數，例如使用資料壓縮的 hello 轉碼器。 這些案例的更多詳細資料中所述，而且 hello 下列程式碼範例所示：

## <a name="install-avro-library"></a>安裝 Avro Library
hello 下列是必要的然後再安裝 hello 程式庫：

* <a href="http://www.microsoft.com/download/details.aspx?id=17851" target="_blank">Microsoft .NET Framework 4</a>
* <a href="http://james.newtonking.com/json" target="_blank">Newtonsoft Json.NET</a> (6.0.4 或更新版本)

請注意該 hello Newtonsoft.Json.dll 相依性會自動下載 hello Microsoft Avro Library hello 安裝。 hello 程序提供的下列區段的 hello:

以 NuGet 套件，可透過下列程序的 hello 安裝從 Visual Studio 發佈 hello Microsoft Avro Library:

1. 選取 hello**專案** 索引標籤-> **管理 NuGet 封裝...**
2. Hello 中的搜尋 「 Microsoft.Hadoop.Avro"**線上搜尋**方塊。
3. 按一下 hello**安裝**太下一步按鈕**Microsoft Azure HDInsight Avro Library**。

請注意該 hello Newtonsoft.Json.dll (> = 6.0.4) 相依性也會自動下載以 hello Microsoft Avro Library。

hello Microsoft Avro Library 原始程式碼位於[Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro)。

## <a name="compile-schemas-using-avro-library"></a>使用 Avro Library 來編譯結構描述
hello Microsoft Avro Library 包含公用程式，讓建立 C# 類型會自動根據 hello 先前定義的 JSON 結構描述產生程式碼。 hello 程式碼產生公用程式可執行檔的二進位檔分散，但是可以透過下列程序的 hello 使用者輕鬆建立：

1. 下載 HDInsight SDK 中的原始程式碼 hello 最新版本的 hello.zip 檔案<a href="http://hadoopsdk.codeplex.com/SourceControl/latest#" target="_blank">Microsoft.NET SDK 的 Hadoop</a>。 (按一下 hello**下載**圖示，不 hello**下載** 索引標籤。)
2. 擷取的 hello HDInsight SDK tooa 目錄 hello 與.NET Framework 4 的電腦上安裝和 toohello 網際網路連線下載必要的依存性 NuGet 封裝。 以下，我們假設 hello 原始程式碼擷取的 tooC:\SDK。
3. 移 toohello 資料夾 C:\SDK\src\Microsoft.Hadoop.Avro.Tools 並執行 build.bat。 （hello 檔案呼叫 MSBuild 從 hello 32 位元發佈的 hello.NET Framework。 如果您想要 toouse hello 64 位元版本中，編輯 build.bat 下列 hello hello 檔案內的註解。)確保 hello 建置成功完成。 (在某些系統上，MSBuild 可能會產生警告。 這些警告不會影響 hello 公用程式，只要不有任何建置錯誤。）
4. hello 編譯公用程式位於 C:\SDK\Bin\Unsigned\Release\Microsoft.Hadoop.Avro.Tools。

tooget 熟悉 hello 命令列語法中，執行 hello hello hello 程式碼產生公用程式所在的資料夾中的下列命令：`Microsoft.Hadoop.Avro.Tools help /c:codegen`

tootest hello 公用程式，您可以從 hello 範例 JSON 結構描述檔案隨附 hello 原始程式碼產生 C# 類別。 執行下列命令的 hello:

    Microsoft.Hadoop.Avro.Tools codegen /i:C:\SDK\src\Microsoft.Hadoop.Avro.Tools\SampleJSON\SampleJSONSchema.avsc /o:

這應該 tooproduce 兩個 C# 檔案 hello 目前目錄中： SensorData.cs 和 Location.cs。

toounderstand hello 邏輯 hello 程式碼產生公用程式所使用時轉換 hello JSON 結構描述 tooC # 型別，請參閱 GenerationVerification.feature 位於 C:\SDK\src\Microsoft.Hadoop.Avro.Tools\Doc hello 檔案。

命名空間會擷取從 hello JSON 結構描述，使用 hello 邏輯 hello 前段中所述的 hello 檔案中所述。 擷取從 hello 結構描述的命名空間會優先於任何隨附 hello 公用程式命令列中的 hello /n 參數。 如果您想 hello 結構描述中包含的 toooverride hello 命名空間，請使用 hello /nf 參數。 例如，toochange hello SampleJSONSchema.avsc toomy.own.nspace 的所有命名空間執行 hello 下列命令：

    Microsoft.Hadoop.Avro.Tools codegen /i:C:\SDK\src\Microsoft.Hadoop.Avro.Tools\SampleJSON\SampleJSONSchema.avsc /o:. /nf:my.own.nspace

## <a name="about-hello-samples"></a>有關 hello 範例
本主題提供的六個範例說明不同 hello Microsoft Avro Library 所支援的案例。 hello Microsoft Avro Library 是設計的 toowork 與任何資料流。 為了方便一致起見，這些範例會透過記憶體資料流，而不是檔案資料流或資料庫。 在實際執行環境中所採取的 hello 方法，取決於 hello 確切情況的需求、 資料來源和磁碟區、 效能限制，以及其他因素。

hello 第兩個範例顯示如何 tooserialize 和記憶體資料流緩衝區的資料序列化使用反映和泛用記錄。 hello 結構描述兩種情況中的會假設 toobe hello 讀取器和寫入器之間共用的頻外。

hello 第三個和第四個範例顯示如何 tooserialize 和還原序列化資料，藉由使用 hello Avro 物件容器檔案。 當資料儲存在 Avro 容器檔案中時，會一律儲存其結構描述與其因為 hello 結構描述必須共用的還原序列化。

hello 範例包含 hello 前四個範例可從 hello 下載<a href="http://code.msdn.microsoft.com/Serialize-data-with-the-86055923" target="_blank">Azure 程式碼範例</a>站台。

hello 第五個範例會示範如何自訂壓縮轉碼器的 Avro toouse 物件容器檔案。 您可以從 hello 下載這個範例包含 hello 程式碼範例<a href="http://code.msdn.microsoft.com/Serialize-data-with-the-67159111" target="_blank">Azure 程式碼範例</a>站台。

hello 第六個範例顯示如何 toouse Avro 序列化 tooupload 資料 tooAzure Blob 儲存體，然後使用 Hive (Hadoop) HDInsight 叢集與分析。 它可以從 hello 下載<a href="https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3" target="_blank">Azure 程式碼範例</a>站台。

以下是連結 toohello hello 主題所述的六個範例：

* <a href="#Scenario1">**使用反映的序列化**</a> -hello 類型 toobe 序列化的 JSON 結構描述會自動建置 hello 資料合約屬性。
* <a href="#Scenario2">**與泛型記錄序列化**</a> -可供反映任何.NET 型別時，在記錄中明確指定 hello JSON 結構描述。
* <a href="#Scenario3">**使用物件容器的檔案，使用反映的序列化**</a> -hello JSON 結構描述會自動建立並共用以及透過 Avro 物件容器檔 hello 序列化資料。
* <a href="#Scenario4">**序列化物件容器檔案使用一般記錄**</a> -hello JSON 結構描述會明確地指定 hello 序列化之前並搭配 hello 資料透過 Avro 物件容器的檔案共用。
* <a href="#Scenario5">**序列化使用的自訂壓縮轉碼器的物件容器檔案**</a> -hello 範例將示範如何 toocreate Avro 物件具有自訂.NET 實作的 hello Deflate 資料壓縮轉碼器容器檔案。
* <a href="#Scenario6">**使用 Avro tooupload 資料的 Microsoft Azure HDInsight 服務的 hello** </a> -hello 範例說明 Avro 序列化與 hello HDInsight 服務的互動方式。 使用中 Azure 訂用帳戶和存取 tooan Azure HDInsight 叢集需要 toorun 這個範例。

## <a name="Scenario1"></a>範例 1：使用反映進行序列化
hello hello 類型的 JSON 結構描述會自動由建置 hello Microsoft Avro Library 透過反映來從 hello 資料合約的 hello C# 物件 toobe 序列化的屬性。 hello Microsoft Avro Library 建立[ **IAvroSeralizer<T>**  ](http://msdn.microsoft.com/library/dn627341.aspx) tooidentify hello 欄位 toobe 序列化。

在此範例中，物件 ( **SensorData**類別成員**位置**結構) 是序列化的 tooa 記憶體資料流，並接著會還原序列化此資料流。 hello 結果是，則比較的 toohello 初始執行個體 tooconfirm 該 hello **SensorData**物件復原為原始的相同 toohello。

在此範例中的 hello 結構描述會假設 toobe 共用之間 hello 讀取器和寫入器，因此不需要 hello Avro 物件的容器格式。 如需如何 tooserialize 和還原序列化資料到記憶體緩衝區 hello 結構描述必須共用 hello 資料時，使用反映來與 hello 物件容器格式，請參閱<a href="#Scenario3">序列化使用反映物件容器的檔案</a>.

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro;

        //Sample class used in serialization samples
        [DataContract(Name = "SensorDataValue", Namespace = "Sensors")]
        internal class SensorData
        {
            [DataMember(Name = "Location")]
            public Location Position { get; set; }

            [DataMember(Name = "Value")]
            public byte[] Value { get; set; }
        }

        //Sample struct used in serialization samples
        [DataContract]
        internal struct Location
        {
            [DataMember]
            public int Floor { get; set; }

            [DataMember]
            public int Room { get; set; }
        }

        //This class contains all methods demonstrating
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serialize and deserialize sample data set represented as an object using reflection.
            //No explicit schema definition is required - schema of serialized objects is automatically built.
            public void SerializeDeserializeObjectUsingReflection()
            {

                Console.WriteLine("SERIALIZATION USING REFLECTION\n");
                Console.WriteLine("Serializing Sample Data Set...");

                //Create a new AvroSerializer instance and specify a custom serialization strategy AvroDataContractResolver
                //for serializing only properties attributed with DataContract/DateMember
                var avroSerializer = AvroSerializer.Create<SensorData>();

                //Create a memory stream buffer
                using (var buffer = new MemoryStream())
                {
                    //Create a data set by using sample class and struct
                    var expected = new SensorData { Value = new byte[] { 1, 2, 3, 4, 5 }, Position = new Location { Room = 243, Floor = 1 } };

                    //Serialize hello data toohello specified stream
                    avroSerializer.Serialize(buffer, expected);


                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Deserialize data from hello stream and cast it toohello same type used for serialization
                    var actual = avroSerializer.Deserialize(buffer);

                    Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                    //Finally, verify that deserialized data matches hello original one
                    bool isEqual = this.Equal(expected, actual);

                    Console.WriteLine("Result of Data Set Identity Comparison is {0}", isEqual);

                }
            }

            //
            //Helper methods
            //

            //Comparing two SensorData objects
            private bool Equal(SensorData left, SensorData right)
            {
                return left.Position.Equals(right.Position) && left.Value.SequenceEqual(right.Value);
            }



            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of AvroSample Class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization toomemory using reflection
                Sample.SerializeDeserializeObjectUsingReflection();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING REFLECTION
    //
    // Serializing Sample Data Set...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // Result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.


## <a name="sample-2-serialization-with-a-generic-record"></a>範例 2：使用一般記錄進行序列化
無法使用反映，因為無法 hello 資料表示透過.NET 類別，具有資料合約時，JSON 結構描述，可以明確指定泛型記錄中。 此方法較使用反映來得慢。 在這種情況下，hello hello 資料的結構描述也可能是動態的也就是在編譯時期未知。 資料表示為逗號分隔值 (CSV) 檔案的結構描述才會知道它會轉換 toohello Avro 格式，在執行階段是這類動態案例的範例。

這個範例會示範如何 toocreate 並用[ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) tooexplicitly 方式指定 JSON 結構描述，toopopulate 它與 hello 資料，然後如何 tooserialize 加以還原序列化。 然後比較結果 hello toohello hello 復原記錄的初始執行個體 tooconfirm 是相同的原始 toohello。

在此範例中的 hello 結構描述會假設 toobe 共用之間 hello 讀取器和寫入器，因此不需要 hello Avro 物件的容器格式。 如需如何 tooserialize 和還原序列化資料到記憶體緩衝區 hello 結構描述必須是包含 hello 序列化資料時，使用泛型的記錄與 hello 物件容器格式，請參閱 hello<a href="#Scenario4">使用物件容器的序列化檔案與泛用記錄</a>範例。

    namespace Microsoft.Hadoop.Avro.Sample
    {
    using System;
    using System.Collections.Generic;
    using System.IO;
    using System.Linq;
    using System.Runtime.Serialization;
    using Microsoft.Hadoop.Avro.Container;
    using Microsoft.Hadoop.Avro.Schema;
    using Microsoft.Hadoop.Avro;

    //This class contains all methods demonstrating
    //hello usage of Microsoft Avro Library
    public class AvroSample
    {

        //Serialize and deserialize sample data set by using a generic record.
        //A generic record is a special class with hello schema explicitly defined in JSON.
        //All serialized data should be mapped toohello fields of hello generic record,
        //which in turn is then serialized.
        public void SerializeDeserializeObjectUsingGenericRecords()
        {
            Console.WriteLine("SERIALIZATION USING GENERIC RECORD\n");
            Console.WriteLine("Defining hello Schema and creating Sample Data Set...");

            //Define hello schema in JSON
            const string Schema = @"{
                                ""type"":""record"",
                                ""name"":""Microsoft.Hadoop.Avro.Specifications.SensorData"",
                                ""fields"":
                                    [
                                        {
                                            ""name"":""Location"",
                                            ""type"":
                                                {
                                                    ""type"":""record"",
                                                    ""name"":""Microsoft.Hadoop.Avro.Specifications.Location"",
                                                    ""fields"":
                                                        [
                                                            { ""name"":""Floor"", ""type"":""int"" },
                                                            { ""name"":""Room"", ""type"":""int"" }
                                                        ]
                                                }
                                        },
                                        { ""name"":""Value"", ""type"":""bytes"" }
                                    ]
                            }";

            //Create a generic serializer based on hello schema
            var serializer = AvroSerializer.CreateGeneric(Schema);
            var rootSchema = serializer.WriterSchema as RecordSchema;

            //Create a memory stream buffer
            using (var stream = new MemoryStream())
            {
                //Create a generic record toorepresent hello data
                dynamic location = new AvroRecord(rootSchema.GetField("Location").TypeSchema);
                location.Floor = 1;
                location.Room = 243;

                dynamic expected = new AvroRecord(serializer.WriterSchema);
                expected.Location = location;
                expected.Value = new byte[] { 1, 2, 3, 4, 5 };

                Console.WriteLine("Serializing Sample Data Set...");

                //Serialize hello data
                serializer.Serialize(stream, expected);

                stream.Seek(0, SeekOrigin.Begin);

                Console.WriteLine("Deserializing Sample Data Set...");

                //Deserialize hello data into a generic record
                dynamic actual = serializer.Deserialize(stream);

                Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                //Finally, verify hello results
                bool isEqual = expected.Location.Floor.Equals(actual.Location.Floor);
                isEqual = isEqual && expected.Location.Room.Equals(actual.Location.Room);
                isEqual = isEqual && ((byte[])expected.Value).SequenceEqual((byte[])actual.Value);
                Console.WriteLine("Result of Data Set Identity Comparison is {0}", isEqual);
            }
        }

        static void Main()
        {

            string sectionDivider = "---------------------------------------- ";

            //Create an instance of AvroSample class and invoke methods
            //illustrating different serializing approaches
            AvroSample Sample = new AvroSample();

            //Serialization toomemory using generic record
            Sample.SerializeDeserializeObjectUsingGenericRecords();

            Console.WriteLine(sectionDivider);
            Console.WriteLine("Press any key tooexit.");
            Console.Read();
        }
    }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING GENERIC RECORD
    //
    // Defining hello Schema and creating Sample Data Set...
    // Serializing Sample Data Set...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // Result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.


## <a name="sample-3-serialization-using-object-container-files-and-serialization-with-reflection"></a>範例 3：使用物件容器檔案進行序列化和使用反映進行序列化
這個範例是類似的 toohello 案例在 hello<a href="#Scenario1">第一個範例</a>，隱含地使用反映指定 hello 結構描述。 hello 差異是，在這裡，hello 結構描述不會被 toobe 已知 toohello 讀取器將它還原序列化。 hello **SensorData**序列化的物件 toobe 和其隱含指定的結構描述會儲存在由 hello Avro 物件容器檔案[ **AvroContainer** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx)類別。

這個範例中序列化的 hello 資料[ **SequentialWriter<SensorData>**  ](http://msdn.microsoft.com/library/dn627340.aspx)及使用已還原序列化[ **SequentialReader<SensorData>** ](http://msdn.microsoft.com/library/dn627340.aspx). hello 結果則是比較的 toohello 初始執行個體 tooensure 身分識別。

hello hello 中的資料物件透過 hello 預設會壓縮容器檔[ **Deflate** ] [ deflate-100]壓縮轉碼器，從.NET Framework 4。 請參閱 hello<a href="#Scenario5">第五個範例</a>在這個主題 toolearn 如何 toouse 最新且更好的版的 hello [ **Deflate** ] [ deflate-110]壓縮.NET Framework 4.5 中可用的轉碼器。

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro;

        //Sample class used in serialization samples
        [DataContract(Name = "SensorDataValue", Namespace = "Sensors")]
        internal class SensorData
        {
            [DataMember(Name = "Location")]
            public Location Position { get; set; }

            [DataMember(Name = "Value")]
            public byte[] Value { get; set; }
        }

        //Sample struct used in serialization samples
        [DataContract]
        internal struct Location
        {
            [DataMember]
            public int Floor { get; set; }

            [DataMember]
            public int Room { get; set; }
        }

        //This class contains all methods demonstrating
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes hello sample data set by using reflection and Avro object container files.
            //Serialized data is compressed with hello Deflate codec.
            public void SerializeDeserializeUsingObjectContainersReflection()
            {

                Console.WriteLine("SERIALIZATION USING REFLECTION AND AVRO OBJECT CONTAINER FILES\n");

                //Path for Avro object container file
                string path = "AvroSampleReflectionDeflate.avro";

                //Create a data set by using sample class and struct
                var testData = new List<SensorData>
                        {
                            new SensorData { Value = new byte[] { 1, 2, 3, 4, 5 }, Position = new Location { Room = 243, Floor = 1 } },
                            new SensorData { Value = new byte[] { 6, 7, 8, 9 }, Position = new Location { Room = 244, Floor = 1 } }
                        };

                //Serializing and saving data toofile.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects toostream.
                    //Data is compressed using hello Deflate codec.
                    using (var w = AvroContainer.CreateWriter<SensorData>(buffer, Codec.Deflate))
                    {
                        using (var writer = new SequentialWriter<SensorData>(w, 24))
                        {
                            // Serialize hello data toostream by using hello sequential writer
                            testData.ForEach(writer.Write);
                        }
                    }

                    //Save stream toofile
                    Console.WriteLine("Saving serialized data toofile...");
                    if (!WriteFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }
                }

                //Reading and deserializing data.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Reading data from file...");

                    //Reading data from object container file
                    if (!ReadFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }

                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from hello given stream.
                    //It allows iterating over hello deserialized objects because it implements hello IEnumerable<T> interface.
                    using (var reader = new SequentialReader<SensorData>(
                        AvroContainer.CreateReader<SensorData>(buffer, true)))
                    {
                        var results = reader.Objects;

                        //Finally, verify that deserialized data matches hello original one
                        Console.WriteLine("Comparing Initial and Deserialized Data Sets...");
                        int count = 1;
                        var pairs = testData.Zip(results, (serialized, deserialized) => new { expected = serialized, actual = deserialized });
                        foreach (var pair in pairs)
                        {
                            bool isEqual = this.Equal(pair.expected, pair.actual);
                            Console.WriteLine("For Pair {0} result of Data Set Identity Comparison is {1}", count, isEqual);
                            count++;
                        }
                    }
                }

                //Delete hello file
                RemoveFile(path);
            }

            //
            //Helper methods
            //

            //Comparing two SensorData objects
            private bool Equal(SensorData left, SensorData right)
            {
                return left.Position.Equals(right.Position) && left.Value.SequenceEqual(right.Value);
            }

            //Saving memory stream tooa new file with hello given path
            private bool WriteFile(MemoryStream InputStream, string path)
            {
                if (!File.Exists(path))
                {
                    try
                    {
                        using (FileStream fs = File.Create(path))
                        {
                            InputStream.Seek(0, SeekOrigin.Begin);
                            InputStream.CopyTo(fs);
                        }
                        return true;
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during creation and writing toohello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                        return false;
                    }
                }
                else
                {
                    Console.WriteLine("Can not create file \"{0}\". File already exists", path);
                    return false;

                }
            }

            //Reading a file content by using hello given path tooa memory stream
            private bool ReadFile(MemoryStream OutputStream, string path)
            {
                try
                {
                    using (FileStream fs = File.Open(path, FileMode.Open))
                    {
                        fs.CopyTo(OutputStream);
                    }
                    return true;
                }
                catch (Exception e)
                {
                    Console.WriteLine("hello following exception was thrown during reading from hello file \"{0}\"", path);
                    Console.WriteLine(e.Message);
                    return false;
                }
            }

            //Deleting file by using given path
            private void RemoveFile(string path)
            {
                if (File.Exists(path))
                {
                    try
                    {
                        File.Delete(path);
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during deleting hello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                    }
                }
                else
                {
                    Console.WriteLine("Can not delete file \"{0}\". File does not exist", path);
                }
            }

            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of AvroSample class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization using reflection tooAvro object container file
                Sample.SerializeDeserializeUsingObjectContainersReflection();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING REFLECTION AND AVRO OBJECT CONTAINER FILES
    //
    // Serializing Sample Data Set...
    // Saving serialized data toofile...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    // For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.


## <a name="sample-4-serialization-using-object-container-files-and-serialization-with-generic-record"></a>範例 4：使用物件容器檔案進行序列化和使用一般記錄進行序列化
這個範例是類似的 toohello 案例在 hello<a href="#Scenario2">第二個範例</a>，明確地使用 JSON 指定 hello 結構描述。 hello 差異是，在這裡，hello 結構描述不會被 toobe 已知 toohello 讀取器將它還原序列化。

hello 測試收集的資料集是一份到[ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx)透過明確定義的 JSON 結構描述物件，然後儲存在 hello 所代表的物件容器檔案[ **AvroContainer** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx)類別。 此容器檔案建立的寫入器是使用的 tooserialize hello 資料，未壓縮，然後儲存檔案 tooa tooa 記憶體資料流。 hello [ **Codec.Null** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.codec.null.aspx)建立 hello 讀取器時所使用的參數會指定，這項資料不會壓縮。

hello 資料是從 hello 檔案讀取，然後還原序列化為物件的集合。 這個集合是比較的 toohello 最初 Avro 記錄 tooconfirm 它們完全相同的清單。

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro.Schema;
        using Microsoft.Hadoop.Avro;

        //This class contains all methods demonstrating
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes a sample data set by using a generic record and Avro object container files.
            //Serialized data is not compressed.
            public void SerializeDeserializeUsingObjectContainersGenericRecord()
            {
                Console.WriteLine("SERIALIZATION USING GENERIC RECORD AND AVRO OBJECT CONTAINER FILES\n");

                //Path for Avro object container file
                string path = "AvroSampleGenericRecordNullCodec.avro";

                Console.WriteLine("Defining hello Schema and creating Sample Data Set...");

                //Define hello schema in JSON
                const string Schema = @"{
                                ""type"":""record"",
                                ""name"":""Microsoft.Hadoop.Avro.Specifications.SensorData"",
                                ""fields"":
                                    [
                                        {
                                            ""name"":""Location"",
                                            ""type"":
                                                {
                                                    ""type"":""record"",
                                                    ""name"":""Microsoft.Hadoop.Avro.Specifications.Location"",
                                                    ""fields"":
                                                        [
                                                            { ""name"":""Floor"", ""type"":""int"" },
                                                            { ""name"":""Room"", ""type"":""int"" }
                                                        ]
                                                }
                                        },
                                        { ""name"":""Value"", ""type"":""bytes"" }
                                    ]
                            }";

                //Create a generic serializer based on hello schema
                var serializer = AvroSerializer.CreateGeneric(Schema);
                var rootSchema = serializer.WriterSchema as RecordSchema;

                //Create a generic record toorepresent hello data
                var testData = new List<AvroRecord>();

                dynamic expected1 = new AvroRecord(rootSchema);
                dynamic location1 = new AvroRecord(rootSchema.GetField("Location").TypeSchema);
                location1.Floor = 1;
                location1.Room = 243;
                expected1.Location = location1;
                expected1.Value = new byte[] { 1, 2, 3, 4, 5 };
                testData.Add(expected1);

                dynamic expected2 = new AvroRecord(rootSchema);
                dynamic location2 = new AvroRecord(rootSchema.GetField("Location").TypeSchema);
                location2.Floor = 1;
                location2.Room = 244;
                expected2.Location = location2;
                expected2.Value = new byte[] { 6, 7, 8, 9 };
                testData.Add(expected2);

                //Serializing and saving data toofile.
                //Create a MemoryStream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects toostream.
                    //Data is not compressed (Null compression codec).
                    using (var writer = AvroContainer.CreateGenericWriter(Schema, buffer, Codec.Null))
                    {
                        using (var streamWriter = new SequentialWriter<object>(writer, 24))
                        {
                            // Serialize hello data toostream by using hello sequential writer
                            testData.ForEach(streamWriter.Write);
                        }
                    }

                    Console.WriteLine("Saving serialized data toofile...");

                    //Save stream toofile
                    if (!WriteFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }
                }

                //Reading and deserializing hello data.
                //Create a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Reading data from file...");

                    //Reading data from object container file
                    if (!ReadFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }

                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from hello given stream.
                    //It allows iterating over hello deserialized objects because it implements hello IEnumerable<T> interface.
                    using (var reader = AvroContainer.CreateGenericReader(buffer))
                    {
                        using (var streamReader = new SequentialReader<object>(reader))
                        {
                            var results = streamReader.Objects;

                            Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                            //Finally, verify hello results
                            var pairs = testData.Zip(results, (serialized, deserialized) => new { expected = (dynamic)serialized, actual = (dynamic)deserialized });
                            int count = 1;
                            foreach (var pair in pairs)
                            {
                                bool isEqual = pair.expected.Location.Floor.Equals(pair.actual.Location.Floor);
                                isEqual = isEqual && pair.expected.Location.Room.Equals(pair.actual.Location.Room);
                                isEqual = isEqual && ((byte[])pair.expected.Value).SequenceEqual((byte[])pair.actual.Value);
                                Console.WriteLine("For Pair {0} result of Data Set Identity Comparison is {1}", count, isEqual.ToString());
                                count++;
                            }
                        }
                    }
                }

                //Delete hello file
                RemoveFile(path);
            }

            //
            //Helper methods
            //

            //Saving memory stream tooa new file with hello given path
            private bool WriteFile(MemoryStream InputStream, string path)
            {
                if (!File.Exists(path))
                {
                    try
                    {
                        using (FileStream fs = File.Create(path))
                        {
                            InputStream.Seek(0, SeekOrigin.Begin);
                            InputStream.CopyTo(fs);
                        }
                        return true;
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during creation and writing toohello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                        return false;
                    }
                }
                else
                {
                    Console.WriteLine("Can not create file \"{0}\". File already exists", path);
                    return false;

                }
            }

            //Reading a file content by using hello given path tooa memory stream
            private bool ReadFile(MemoryStream OutputStream, string path)
            {
                try
                {
                    using (FileStream fs = File.Open(path, FileMode.Open))
                    {
                        fs.CopyTo(OutputStream);
                    }
                    return true;
                }
                catch (Exception e)
                {
                    Console.WriteLine("hello following exception was thrown during reading from hello file \"{0}\"", path);
                    Console.WriteLine(e.Message);
                    return false;
                }
            }

            //Deleting file by using hello given path
            private void RemoveFile(string path)
            {
                if (File.Exists(path))
                {
                    try
                    {
                        File.Delete(path);
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during deleting hello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                    }
                }
                else
                {
                    Console.WriteLine("Can not delete file \"{0}\". File does not exist", path);
                }
            }

            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of hello AvroSample class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization using generic record tooAvro object container file
                Sample.SerializeDeserializeUsingObjectContainersGenericRecord();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING GENERIC RECORD AND AVRO OBJECT CONTAINER FILES
    //
    // Defining hello Schema and creating Sample Data Set...
    // Serializing Sample Data Set...
    // Saving serialized data toofile...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    // For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.




## <a name="sample-5-serialization-using-object-container-files-with-a-custom-compression-codec"></a>範例 5：使用物件容器檔案和自訂壓縮轉碼器進行序列化
hello 第五個範例會示範如何自訂壓縮轉碼器的 Avro toouse 物件容器檔案。 您可以從 hello 下載這個範例包含 hello 程式碼範例[Azure 程式碼範例](http://code.msdn.microsoft.com/Serialize-data-with-the-67159111)站台。

hello [Avro 規格](http://avro.apache.org/docs/current/spec.html#Required+Codecs)允許選擇性壓縮轉碼器的使用方式 (除了太**Null**和**Deflate**預設值)。 此範例中不會實作新的轉碼器，例如 Snappy (提及是支援的選擇性轉碼器在 hello [Avro 規格](http://avro.apache.org/docs/current/spec.html#snappy))。 它會顯示如何 toouse hello hello 的.NET Framework 4.5 實作[ **Deflate** ] [ deflate-110]轉碼器，提供更好的壓縮演算法，根據 hello [zlib](http://zlib.net/) hello 預設.NET Framework 4 版本比壓縮程式庫。

    //
    // This code needs toobe compiled with hello parameter Target Framework set as ".NET Framework 4.5"
    // tooensure hello desired implementation of hello Deflate compression algorithm is used.
    // Ensure your C# project is set up accordingly.
    //

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.IO;
        using System.IO.Compression;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro;

        #region Defining objects for serialization
        //Sample class used in serialization samples
        [DataContract(Name = "SensorDataValue", Namespace = "Sensors")]
        internal class SensorData
        {
            [DataMember(Name = "Location")]
            public Location Position { get; set; }

            [DataMember(Name = "Value")]
            public byte[] Value { get; set; }
        }

        //Sample struct used in serialization samples
        [DataContract]
        internal struct Location
        {
            [DataMember]
            public int Floor { get; set; }

            [DataMember]
            public int Room { get; set; }
        }
        #endregion

        #region Defining custom codec based on .NET Framework V.4.5 Deflate
        //Avro.NET codec class contains two methods,
        //GetCompressedStreamOver(Stream uncompressed) and GetDecompressedStreamOver(Stream compressed),
        //which are hello key ones for data compression.
        //tooenable a custom codec, one needs tooimplement these methods for hello required codec.

        #region Defining Compression and Decompression Streams
        //DeflateStream (class from System.IO.Compression namespace that implements Deflate algorithm)
        //cannot be directly used for Avro because it does not support vital operations like Seek.
        //Thus one needs tooimplement two classes inherited from stream
        //(one for compressed and one for decompressed stream)
        //that use Deflate compression and implement all required features.
        internal sealed class CompressionStreamDeflate45 : Stream
        {
            private readonly Stream buffer;
            private DeflateStream compressionStream;

            public CompressionStreamDeflate45(Stream buffer)
            {
                Debug.Assert(buffer != null, "Buffer is not allowed toobe null.");

                this.compressionStream = new DeflateStream(buffer, CompressionLevel.Fastest, true);
                this.buffer = buffer;
            }

            public override bool CanRead
            {
                get { return this.buffer.CanRead; }
            }

            public override bool CanSeek
            {
                get { return true; }
            }

            public override bool CanWrite
            {
                get { return this.buffer.CanWrite; }
            }

            public override void Flush()
            {
                this.compressionStream.Close();
            }

            public override long Length
            {
                get { return this.buffer.Length; }
            }

            public override long Position
            {
                get
                {
                    return this.buffer.Position;
                }

                set
                {
                    this.buffer.Position = value;
                }
            }

            public override int Read(byte[] buffer, int offset, int count)
            {
                return this.buffer.Read(buffer, offset, count);
            }

            public override long Seek(long offset, SeekOrigin origin)
            {
                return this.buffer.Seek(offset, origin);
            }

            public override void SetLength(long value)
            {
                throw new NotSupportedException();
            }

            public override void Write(byte[] buffer, int offset, int count)
            {
                this.compressionStream.Write(buffer, offset, count);
            }

            protected override void Dispose(bool disposed)
            {
                base.Dispose(disposed);

                if (disposed)
                {
                    this.compressionStream.Dispose();
                    this.compressionStream = null;
                }
            }
        }

        internal sealed class DecompressionStreamDeflate45 : Stream
        {
            private readonly DeflateStream decompressed;

            public DecompressionStreamDeflate45(Stream compressed)
            {
                this.decompressed = new DeflateStream(compressed, CompressionMode.Decompress, true);
            }

            public override bool CanRead
            {
                get { return true; }
            }

            public override bool CanSeek
            {
                get { return true; }
            }

            public override bool CanWrite
            {
                get { return false; }
            }

            public override void Flush()
            {
                this.decompressed.Close();
            }

            public override long Length
            {
                get { return this.decompressed.Length; }
            }

            public override long Position
            {
                get
                {
                    return this.decompressed.Position;
                }

                set
                {
                    throw new NotSupportedException();
                }
            }

            public override int Read(byte[] buffer, int offset, int count)
            {
                return this.decompressed.Read(buffer, offset, count);
            }

            public override long Seek(long offset, SeekOrigin origin)
            {
                throw new NotSupportedException();
            }

            public override void SetLength(long value)
            {
                throw new NotSupportedException();
            }

            public override void Write(byte[] buffer, int offset, int count)
            {
                throw new NotSupportedException();
            }

            protected override void Dispose(bool disposing)
            {
                base.Dispose(disposing);

                if (disposing)
                {
                    this.decompressed.Dispose();
                }
            }
        }
        #endregion

        #region Define Codec
        //Define hello actual codec class containing hello required methods for manipulating streams:
        //GetCompressedStreamOver(Stream uncompressed) and GetDecompressedStreamOver(Stream compressed).
        //Codec class uses classes for compressed and decompressed streams defined above.
        internal sealed class DeflateCodec45 : Codec
        {

            //We merely use different IMPLEMENTATIONS of Deflate, so CodecName remains "deflate"
            public static readonly string CodecName = "deflate";

            public DeflateCodec45()
                : base(CodecName)
            {
            }

            public override Stream GetCompressedStreamOver(Stream decompressed)
            {
                if (decompressed == null)
                {
                    throw new ArgumentNullException("decompressed");
                }

                return new CompressionStreamDeflate45(decompressed);
            }

            public override Stream GetDecompressedStreamOver(Stream compressed)
            {
                if (compressed == null)
                {
                    throw new ArgumentNullException("compressed");
                }

                return new DecompressionStreamDeflate45(compressed);
            }
        }
        #endregion

        #region Define modified Codec Factory
        //Define modified codec factory toobe used in hello reader.
        //It catches hello attempt toouse "Deflate" and provide  a custom codec.
        //For all other cases, it relies on hello base class (CodecFactory).
        internal sealed class CodecFactoryDeflate45 : CodecFactory
        {

            public override Codec Create(string codecName)
            {
                if (codecName == DeflateCodec45.CodecName)
                    return new DeflateCodec45();
                else
                    return base.Create(codecName);
            }
        }
        #endregion

        #endregion

        #region Sample Class with demonstration methods
        //This class contains methods demonstrating
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes sample data set by using reflection and Avro object container files.
            //Serialized data is compressed with hello custom compression codec (Deflate of .NET Framework 4.5).
            //
            //This sample uses memory stream for all operations related tooserialization, deserialization and
            //object container manipulation, though file stream could be easily used.
            public void SerializeDeserializeUsingObjectContainersReflectionCustomCodec()
            {

                Console.WriteLine("SERIALIZATION USING REFLECTION, AVRO OBJECT CONTAINER FILES AND CUSTOM CODEC\n");

                //Path for Avro object container file
                string path = "AvroSampleReflectionDeflate45.avro";

                //Create a data set by using sample class and struct
                var testData = new List<SensorData>
                        {
                            new SensorData { Value = new byte[] { 1, 2, 3, 4, 5 }, Position = new Location { Room = 243, Floor = 1 } },
                            new SensorData { Value = new byte[] { 6, 7, 8, 9 }, Position = new Location { Room = 244, Floor = 1 } }
                        };

                //Serializing and saving data toofile.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects toostream.
                    //Here hello custom codec is introduced. For convenience, hello next commented code line shows how toouse built-in Deflate.
                    //Note that because hello sample deals with different IMPLEMENTATIONS of Deflate, built-in and custom codecs are interchangeable
                    //in read-write operations.
                    //using (var w = AvroContainer.CreateWriter<SensorData>(buffer, Codec.Deflate))
                    using (var w = AvroContainer.CreateWriter<SensorData>(buffer, new DeflateCodec45()))
                    {
                        using (var writer = new SequentialWriter<SensorData>(w, 24))
                        {
                            // Serialize hello data toostream using hello sequential writer
                            testData.ForEach(writer.Write);
                        }
                    }

                    //Save stream toofile
                    Console.WriteLine("Saving serialized data toofile...");
                    if (!WriteFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }
                }

                //Reading and deserializing data.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Reading data from file...");

                    //Reading data from object container file
                    if (!ReadFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }

                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Because of SequentialReader<T> constructor signature, an AvroSerializerSettings instance is required
                    //when codec factory is explicitly specified.
                    //You may comment hello line below if you want toouse built-in Deflate (see next comment).
                    AvroSerializerSettings settings = new AvroSerializerSettings();

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from hello given stream.
                    //It allows iterating over hello deserialized objects because it implements hello IEnumerable<T> interface.
                    //Here hello custom codec factory is introduced.
                    //For convenience, hello next commented code line shows how toouse built-in Deflate
                    //(no explicit Codec Factory parameter is required in this case).
                    //Note that because hello sample deals with different IMPLEMENTATIONS of Deflate, built-in and custom codecs are interchangeable
                    //in read-write operations.
                    //using (var reader = new SequentialReader<SensorData>(AvroContainer.CreateReader<SensorData>(buffer, true)))
                    using (var reader = new SequentialReader<SensorData>(
                        AvroContainer.CreateReader<SensorData>(buffer, true, settings, new CodecFactoryDeflate45())))
                    {
                        var results = reader.Objects;

                        //Finally, verify that deserialized data matches hello original one
                        Console.WriteLine("Comparing Initial and Deserialized Data Sets...");
                        bool isEqual;
                        int count = 1;
                        var pairs = testData.Zip(results, (serialized, deserialized) => new { expected = serialized, actual = deserialized });
                        foreach (var pair in pairs)
                        {
                            isEqual = this.Equal(pair.expected, pair.actual);
                            Console.WriteLine("For Pair {0} result of Data Set Identity Comparison is {1}", count, isEqual.ToString());
                            count++;
                        }
                    }
                }

                //Delete hello file
                RemoveFile(path);
            }
        #endregion

            #region Helper Methods

            //Comparing two SensorData objects
            private bool Equal(SensorData left, SensorData right)
            {
                return left.Position.Equals(right.Position) && left.Value.SequenceEqual(right.Value);
            }

            //Saving memory stream tooa new file with hello given path
            private bool WriteFile(MemoryStream InputStream, string path)
            {
                if (!File.Exists(path))
                {
                    try
                    {
                        using (FileStream fs = File.Create(path))
                        {
                            InputStream.Seek(0, SeekOrigin.Begin);
                            InputStream.CopyTo(fs);
                        }
                        return true;
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during creation and writing toohello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                        return false;
                    }
                }
                else
                {
                    Console.WriteLine("Can not create file \"{0}\". File already exists", path);
                    return false;

                }
            }

            //Reading file content by using hello given path tooa memory stream
            private bool ReadFile(MemoryStream OutputStream, string path)
            {
                try
                {
                    using (FileStream fs = File.Open(path, FileMode.Open))
                    {
                        fs.CopyTo(OutputStream);
                    }
                    return true;
                }
                catch (Exception e)
                {
                    Console.WriteLine("hello following exception was thrown during reading from hello file \"{0}\"", path);
                    Console.WriteLine(e.Message);
                    return false;
                }
            }

            //Deleting file by using given path
            private void RemoveFile(string path)
            {
                if (File.Exists(path))
                {
                    try
                    {
                        File.Delete(path);
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during deleting hello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                    }
                }
                else
                {
                    Console.WriteLine("Can not delete file \"{0}\". File does not exist", path);
                }
            }
            #endregion

            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of AvroSample Class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization using reflection tooAvro object container file using custom codec
                Sample.SerializeDeserializeUsingObjectContainersReflectionCustomCodec();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING REFLECTION, AVRO OBJECT CONTAINER FILES AND CUSTOM CODEC
    //
    // Serializing Sample Data Set...
    // Saving serialized data toofile...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    //For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.

## <a name="sample-6-using-avro-tooupload-data-for-hello-microsoft-azure-hdinsight-service"></a>範例 6： 使用 Avro tooupload 資料 hello Microsoft Azure HDInsight 服務
hello 第六個範例將說明一些程式設計技術相關的 toointeracting 與 hello Azure HDInsight 服務。 您可以從 hello 下載這個範例包含 hello 程式碼範例[Azure 程式碼範例](https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3)站台。

hello 範例並未 hello 下列工作：

* 連接 tooan 現有 HDInsight 服務叢集。
* 將序列化多個 CSV 檔案，並上傳 hello 結果 tooAzure Blob 儲存體。 (hello CSV 檔案與 hello 範例一起散發，而且代表擷取自 AMEX 股票的歷程記錄資料散佈[Infochimps](http://www.infochimps.com/) hello 期間從 1970年-2010年。 hello 範例讀取 CSV 檔案資料、 將 hello 的 hello 記錄 tooinstances**股票**類別，並再將它們序列化使用反映。 內建型別定義會建立從透過 hello Microsoft Avro Library 程式碼產生公用程式的 JSON 結構描述。
* 建立新的外部資料表稱為**股票**登錄區，並將它連結 toohello 資料 hello 上一個步驟中上傳。
* 執行查詢，透過使用 Hive hello**股票**資料表。

此外，hello 範例會執行清除程序之前和之後執行主要的作業。 Hello 清除工作期間 hello 的所有相關的 Azure Blob 資料和資料夾會遭到移除，並卸除 hello Hive 資料表。 您也可以叫用 hello hello 範例命令列清除程序。

hello 範例具有 hello 下列必要條件：

* 使用中 Microsoft Azure 訂用帳戶和其訂用帳戶識別碼。
* Hello 相對應的私密金鑰與 hello 訂用帳戶管理憑證。 hello 憑證應該安裝在 hello 目前使用者私人儲存體上 hello 使用機器 toorun hello 範例。
* 使用中 HDInsight 叢集。
* Azure 儲存體帳戶連結從 hello 前一個必要元件，連同 hello 對應的主要或次要存取金鑰 toohello HDInsight 叢集。

Hello 範例在開始執行前，所有 hello hello 必要條件應該是資訊的輸入的 toohello 範例組態檔。 有兩個可能的方式 toodo 它：

* 編輯 hello 範例的根目錄中的 hello app.config 檔案，並再建立 hello 範例
* 第一次建置 hello 範例，然後編輯在 hello 組建目錄中的 AvroHDISample.exe.config

在這兩種情況下，所有的編輯作業應該在 hello  **<appSettings>** 設定 區段。 遵循 hello hello 檔案中的註解。
hello 執行範例時從 hello 命令列執行下列命令 （其中 hello.zip 檔案，與 hello 範例假設已解壓縮的 toobe tooC:\AvroHDISample; 若否則使用 hello 相關檔案路徑） 的 hello:

    AvroHDISample run C:\AvroHDISample\Data

tooclean 向上 hello 叢集，請執行下列命令的 hello:

    AvroHDISample clean

[deflate-100]: http://msdn.microsoft.com/library/system.io.compression.deflatestream(v=vs.100).aspx
[deflate-110]: http://msdn.microsoft.com/library/system.io.compression.deflatestream(v=vs.110).aspx
