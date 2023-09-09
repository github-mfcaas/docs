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
curl --location 'http://my-server/compress' \
--form 'files=@"/C:/data/large-file.txt"' \
--form 'ext="zip"'
`


**C# RestSharp**
`
var client = new RestClient();
var request = new RestRequest("http://my-server/compress", Method.Post);
request.AlwaysMultipartFormData = true;
request.AddFile("files", "/C:/data/large-file.txt");
request.AddParameter("ext", "zip");
RestResponse response = await client.ExecuteAsync(request);
Console.WriteLine(response.Content);
`


**Response**
`
{
    "body": {
        "ext": "zip",
        "files": [
            "licensee_profile.txt"
        ],
        "status": "QUEUED",
        "status_url": "http://10.0.0.109/getstatus?taskid=5a1696e5-d01e-4bc6-85b8-23af3f5febda",
        "taskid": "5a1696e5-d01e-4bc6-85b8-23af3f5febda"
    },
    "headers": {
        "content-type": "application/json"
    },
    "status_code": 200
}
`
