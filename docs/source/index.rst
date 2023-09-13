MFCaaS API Documentation
========================

Managed File Compression as a Service

Do your systems generate 100's or 1000's of log files?

Use our cloud-first approach to file compression by offloading the high CPU and Ram requirements to our system with a single server setup or a cluster of servers. Let us worry about file compression so you can get back to your business.

.. raw:: html
	<p>&nbsp;</p>
	<p>&nbsp;</p>
	<video width="320" height="240" controls>
		<source src="https://github.com/github-mfcaas/docs/blob/main/docs/source/Compress-Request.mp4" type="video/mp4"/>
 		Your browser does not support the video tag.
	</video>
	<p>&nbsp;</p>
	<p>&nbsp;</p>
.. raw:: html
	<p>&nbsp;</p>
	<p>&nbsp;</p>

.. note::

	* This project is under active development.
	* Hosting on Google Cloud, and Microsoft Azure coming soon.
	* 7-Zip compression coming soon.

.. raw:: html
	<p>&nbsp;</p>
	<p>&nbsp;</p>

.. note::
	POSTMAN collection

	https://documenter.getpostman.com/view/29636424/2s9YC1XEzj

.. raw:: html
	<p>&nbsp;</p>
	<p>&nbsp;</p>

Compress a file:
---------------
   Required arguments
      ext
         string: oneof ("gz", "zip", "zst", "br", "xz", "bz2")
      files
         one or more files to compress

.. raw:: html
	<p>&nbsp;</p>
	<p>&nbsp;</p>

Code Examples
-------------


.. parsed-literal::
	**CURL**

	curl --location 'http://my-server/compress' \\ 
		--form 'files=@"/C:/data/large-file.txt"' \\ 
		--form 'ext="zip"' 
	
	curl --location 'http://my-server/compress' \\ 
		--form 'files=@"/C:/data/large-file.txt"' \\ 
		--form 'ext="gz"' 

.. raw:: html
	<p>&nbsp;</p>
	<p>&nbsp;</p>

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

.. raw:: html
	<p>&nbsp;</p>
	<p>&nbsp;</p>

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

.. raw:: html
	<p>&nbsp;</p>
	<p>&nbsp;</p>

.. parsed-literal::

	Fetch your compressed files

	GET http://my-server/getcompletedtask?taskid=5a1696e5-d01e-4bc6-85b8-23af3f5febda

	Returns an application/octet-stream
