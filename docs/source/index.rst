========================
MFCaaS API Documentation
========================

---------------------------------------
*Managed File Compression as a Service*
---------------------------------------


   
   
   
   

Do your systems generate 100's, or 1000's of log files?

Use our cloud-first approach to file compression by offloading the high CPU and Ram requirements to our systems with either a single server or a cluster of servers. Let us worry about file compression so your servers can get back to your business.


   
   
   
   

.. note::

    * This project is under active development.
    * Hosting on Google Cloud, and Microsoft Azure coming soon.
    * 7-Zip compression coming soon.


   
   
   
   

.. note::
    POSTMAN Collection

        https://documenter.getpostman.com/view/29636424/2s9YC1XEzj


   
   
   
   

**Explainer Video**

.. image:: https://github.com/github-mfcaas/docs/raw/main/docs/source/Compress-Request.gif
   :alt: Explainer Video


   
   
   
   

---------------
Compress a file:
---------------

Required arguments

* ext
   * string: oneof ("gz", "zip", "zst", "br", "xz", "bz2")
* files
   * one or more files to compress
      * files can be a single http or https url
      * OR
      * files may be one or more form file posts
   
   
   
   

Code Examples
-------------

* Files for Testing
   * https://gist.githubusercontent.com/github-mfcaas/8a380858c471640210844f5412d0de3a/raw/a9a39202736e9fd0772efc2ad70b8b6f38b9595d/access_log_20230916-114309.log
      * 220 kB
   * https://gist.githubusercontent.com/github-mfcaas/dc5c59f4151ba5a1eabcde92a7c5001e/raw/cb279dfcf5b0d6936f7dc0a49ccf2399ba04199f/access_log_20230916-114317.log
      * 22 MB
   * https://gist.githubusercontent.com/github-mfcaas/31d4e181b3a3d51bcb306c6d5262e007/raw/8209bdd1d0c3fb98db0a89281d73e1074c8b82a3/access_log_20230916-114456.log
      * 44 MB
   * https://gist.github.com/github-mfcaas
      * All test files


.. code-block:: console

   $ curl --location 'http://my-server/compress' \
      --form 'files=@"/C:/data/large-file.txt"' \
      --form 'ext="gz"' 


   $ curl --location 'http://my-server/compress' \
      --form 'files=@"/C:/data/large-file.txt"' \
      --form 'ext="zip"' 



   $ curl --location 'http://my-server/compress' \
      --form 'files=@"/C:/data/large-file.txt"' \
      --form 'files=@"/C:/data/medium-size-file.txt"' \
      --form 'ext="gz"' 


   $ curl --location 'http://my-server/compress' \
      --form 'files=@"/C:/data/large-file.txt"' \
      --form 'files=@"/C:/data/medium-size-file.txt"' \
      --form 'ext="zip"' 


   
   
   
   

.. code-block:: json
   :caption: Response

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

   {
      "body": {
         "ext": "zip",
         "files": [
            "large-file.txt",
            "medium-size-file.txt"
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


   
   
   
   

.. code-block:: json	
   :caption: GetStatus - GET http://my-server/getstatus?taskid=5a1696e5-d01e-4bc6-85b8-23af3f5febda

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


   {
      "body": {
         "datecreated": "2023-09-09 23:33:14",
         "download_url": "http://my-server/getcompletedtask?taskid=5a1696e5-d01e-4bc6-85b8-23af3f5febda",
         "ext": "zip",
         "files": [
            {
               "filename": "large-file.txt",
               "filename": "medium-size-file.txt",
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


   
   
   
   

.. parsed-literal::

    Fetch your compressed files

    GET http://my-server/getcompletedtask?taskid=5a1696e5-d01e-4bc6-85b8-23af3f5febda

    Returns an application/octet-stream, application/x-zip, application/gzip etc.
