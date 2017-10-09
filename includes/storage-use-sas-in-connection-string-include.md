如果您擁有授與存取儲存體帳戶中的 tooresources 共用的存取簽章 (SAS) URL，您可以使用連接字串中的 hello SAS。 Hello SAS 包含 hello 資訊需要的 tooauthenticate hello 要求，因為與 SAS 連接字串提供 hello 通訊協定、 hello 服務端點和 hello 所需的認證 tooaccess hello 資源。

toocreate 連接字串，包含共用的存取簽章指定下列格式的 hello hello 字串：

```
BlobEndpoint=myBlobEndpoint;
QueueEndpoint=myQueueEndpoint;
TableEndpoint=myTableEndpoint;
FileEndpoint=myFileEndpoint;
SharedAccessSignature=sasToken
```

雖然 hello 連接字串必須至少包含一個選擇性的每個服務端點。

> [!NOTE]
> 建議最好搭配使用 HTTPS 與 SAS。
>
> 如果您指定的 SAS 連接字串中的組態檔中，您可能需要 tooencode hello URL 中的特殊字元。
>
>

### <a name="service-sas-example"></a>服務 SAS 範例
以下範例是包含服務 SAS for Blob 儲存體的連接字串：

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
SharedAccessSignature=sv=2015-04-05&sr=b&si=tutorial-policy-635959936145100803&sig=9aCzs76n0E7y5BpEi2GvsSv433BZa22leDOZXX%2BXXIU%3D
```

以下是範例的 hello 和相同的連接字串與特殊字元編碼方式：

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
SharedAccessSignature=sv=2015-04-05&amp;sr=b&amp;si=tutorial-policy-635959936145100803&amp;sig=9aCzs76n0E7y5BpEi2GvsSv433BZa22leDOZXX%2BXXIU%3D
```

### <a name="account-sas-example"></a>帳戶 SAS 範例
以下範例是包含帳戶 SAS for Blob 和檔案儲存體的連接字串。 請注意，指定兩個服務的端點︰

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
FileEndpoint=https://storagesample.file.core.windows.net;
SharedAccessSignature=sv=2015-07-08&sig=iCvQmdZngZNW%2F4vw43j6%2BVz6fndHF5LI639QJba4r8o%3D&spr=https&st=2016-04-12T03%3A24%3A31Z&se=2016-04-13T03%3A29%3A31Z&srt=s&ss=bf&sp=rwl
```

以下是範例的 hello 和相同的連接字串，以 URL 編碼方式：

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
FileEndpoint=https://storagesample.file.core.windows.net;
SharedAccessSignature=sv=2015-07-08&amp;sig=iCvQmdZngZNW%2F4vw43j6%2BVz6fndHF5LI639QJba4r8o%3D&amp;spr=https&amp;st=2016-04-12T03%3A24%3A31Z&amp;se=2016-04-13T03%3A29%3A31Z&amp;srt=s&amp;ss=bf&amp;sp=rwl
```

