MFCaaS API Documentation
========================

Managed File Compression as a Service

Do your systems generate 100's or 1000's of log files?

Use our cloud-first approach to file compression and offload the high CPU and Ram requirements to us. Spin up your own server or cluster of servers and start sending requests. Backed by Amazon AWS, Google Cloud, and MS Azure coming soon!



.. note::

   This project is under active development.
   


Compress a file:
---------------
   Required arguments
      ext
         string: oneof ("gz", "zip")
            other compression types coming soon
      files
         one or more files to compress
            depending on the extension supplied above, the system will create a .zip or a .tar.gz of your files.



Code Examples
-------------



CURL
----
``
   curl --location 'http://my-server/compress' --form 'files=@"/C:/data/large-file.txt"' --form 'ext="zip"'
``






RestSharp
---------
``
      var client = new RestClient();
      var request = new RestRequest("http://my-server/compress", Method.Post);
      request.AlwaysMultipartFormData = true;
      request.AddFile("files", "/C:/data/large-file.txt");
      request.AddParameter("ext", "zip");
      RestResponse response = await client.ExecuteAsync(request);
      Console.WriteLine(response.Content);
``


:Response:
      {
          "body": {
              "ext": "zip",
              "files": [
                  "large-file.txt"
              ],
              "status": "QUEUED",
              "status_url": "http://my-server/getstatus?taskid=5a1696e5-d01e-4bc6-85b8-23af3f5febda",
              "taskid": "5a1696e5-d01e-4bc6-85b8-23af3f5febda"
          },
          "headers": {
              "content-type": "application/json"
          },
          "status_code": 200
      }





.. code-block::
   :caption: GET http://my-server/getstatus?taskid=5a1696e5-d01e-4bc6-85b8-23af3f5febda
      {
          "body": {
              "datecreated": "2023-09-09 23:33:14",
              "download_url": "http://my-server/getcompletedtask?taskid=5a1696e5-d01e-4bc6-85b8-23af3f5febda",
              "ext": "zip",
              "files": [
                  {
                      "filename": "large-file.txt",
                      "id": 430537
                  }
              ],
              "status": "COMPLETED",
              "taskid": "5a1696e5-d01e-4bc6-85b8-23af3f5febda"
          },
          "headers": {
              "content-type": "application/json"
          },
          "status_code": 200
      }
