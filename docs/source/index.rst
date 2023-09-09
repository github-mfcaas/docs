MFCaaS API Documentation
========================

**M**anaged **F**ile **C**ompression as a **S**ervice

.. note::

   This project is under active development.

Contents
--------

**Compress a file**:
   Required arguments
      ext
         string: oneof ("gz", "zip")
            other compression types coming soon
      files
         one or more files to compress
            depending on the extension supplied above the system will return either a .zip or a .tar.gz file

**CURL**
`
curl --location 'http://10.0.0.109/compress' \
--form 'files=@"/C:/data/large-file.txt"' \
--form 'ext="zip"'
`

**C# RestSharp**
`
var options = new RestClientOptions("")
{
  MaxTimeout = -1,
};
var client = new RestClient(options);
var request = new RestRequest("http://10.0.0.109/compress", Method.Post);
request.AlwaysMultipartFormData = true;
request.AddFile("files", "/C:/Users/ericc/mmc/licensee_profile.txt");
request.AddParameter("ext", "zip");
RestResponse response = await client.ExecuteAsync(request);
Console.WriteLine(response.Content);
`
