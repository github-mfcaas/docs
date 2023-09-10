MFCaaS API Documentation
========================

Managed File Compression as a Service
   Do your systems generate 100's or 1000's of log files?
   Use our cloud-first approach to file compression and offload the high CPU and Ram requirements to us.
   Spin up your own server or cluster of servers and start sending requests.
   Backed by Amazon AWS
   Google Cloud, and MS Azure coming soon!



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

.. code-block::
   :caption: CURL
      curl --location 'http://my-server/compress' \
      --form 'files=@"/C:/data/large-file.txt"' \
      --form 'ext="zip"'
