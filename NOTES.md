# NOTES #
Date: 2015-08-05

**Abstract:** The FileTransfer object provides a way to upload files using an HTTP multi-part POST request, and to download files as well.

Documentation source: [cordova-plugin-file-transfer](https://github.com/apache/cordova-plugin-file-transfer/blob/16249c2f7ac53cb593e11eeae180066a88a28271/doc/index.md) <br />
*The documentation source is poorly written, incomplete, & has mistakes.*

Note: `encodeURI()` is native to Javascript.

The **FileTransfer** API has
* one (1) property - `onprogress`
* three (3) methods - `upload`,`download` &amp; `abort`
* two (2)  support objects - `FileUploadResult` &amp;`FileTransferError`

##Properties##
----

This property (callback function) gets appended to the `FileTransfer` object. It appears the purpose of this function is to track transfers.

* `onprogress` gets called-back as the file transfer progresses. The parameters sent to it are not well documented. The W3C documentations says it gets an `eventProgress` object, but it does not list a reference, and these parameters do not match known W3C documents of the same name. The callback parameters are:
 - e.lengthComputable - (boolean) determines if the length of the file is computable
 - e.loaded - (long) running byte count of bytes transfered
 - e.total - (long) total number of bytes to be transfered

NOTES: Parameters derived from the [example code](https://github.com/apache/cordova-plugin-file-transfer/blob/16249c2f7ac53cb593e11eeae180066a88a28271/doc/index.md) in the documentation, and the Java source -&gt;[src/android/FileProgressResult.java](https://github.com/apache/cordova-plugin-file-transfer/blob/16249c2f7ac53cb593e11eeae180066a88a28271/src/android/FileProgressResult.java)

##Methods##
----

###upload (method)###

`upload(fileURL, server, successCallback, errorCallback, options, trustAllHosts);`

* fileURL - Filesystem URL representing the file on the device (NOTE: Many issues. SEE: **Backwards Compatibility Notes** in [docs](https://github.com/apache/cordova-plugin-file-transfer/blob/16249c2f7ac53cb593e11eeae180066a88a28271/doc/index.md))
* server - URL of the server to receive the file, as encoded by `encodeURI()`.
* successCallback - callback receives `FileUploadResult` (Object)
* errorCallback - callback receives `FileTransferError` (Object)
* options -
 - fileKey: The name of the form element. Defaults to file. (DOMString)
 - fileName: The file name to use when saving the file on the server. Defaults to image.jpg. (DOMString)
 - mimeType: The mime type of the data to upload. Defaults to image/jpeg. (DOMString)
 - params: A set of optional key/value pairs to pass in the HTTP request. (Object)
 - chunkedMode: Whether to upload the data in chunked streaming mode. Defaults to true. (Boolean)
 - headers: A map of header name/header values. Use an array to specify more than one value. (Object)
* trustAllHosts (default:false)

###download (method)###

`upload(source, target, successCallback, errorCallback, trustAllHosts, options);`

* source - URL of the server to download the file, as encoded by `encodeURI()`.
* target - Filesystem url representing the file on the device. (NOTE: Many issues. SEE: **Backwards Compatibility Notes** in [docs](https://github.com/apache/cordova-plugin-file-transfer/blob/16249c2f7ac53cb593e11eeae180066a88a28271/doc/index.md))
* successCallback - callback receives `FileEntry` (Object) (SEE: below **FileDownloadResult**)
* errorCallback - callback receives `FileTransferError` (Object)
* trustAllHosts - (default:false)
* options - (vaguely defined as `headers` for "Authorization"; SEE [code example](https://github.com/apache/cordova-plugin-file-transfer/blob/16249c2f7ac53cb593e11eeae180066a88a28271/doc/index.md))

##abort (method)###

`abort()`

* (no parameters)


##Objects##
----

###FileUploadResult (object)###

* bytesSent: The number of bytes sent to the server as part of the upload. (long)
* responseCode: The HTTP response code returned by the server. (long)
* response: The HTTP response returned by the server. (DOMString)
* headers: The HTTP response headers by the server. Currently supported on iOS only. (Object)

iOS does not support 'responseCode' or 'bytesSent'.

###FileDownloadResult (object)###

There is no FileDownloadResult (object). The documentation says a `FileEntry` object will be returned. They mean this [FileEntry](https://github.com/apache/cordova-plugin-file). In turn, the vague details can be found at [HTML5Rocks](http://www.html5rocks.com/en/tutorials/file/filesystem/)

###FileTransferError (object)###

* code: One of the predefined error codes listed below *Constants*. (Number)
* source: URL to the source. (String)
* target: URL to the target. (String)
* http_status: HTTP status code. This attribute is only available when a response code is received from the HTTP connection. (Number)
* exception: Either e.getMessage or e.toString (String)

* Constants (for `code`)
 - 1 = FileTransferError.FILE_NOT_FOUND_ERR
 - 2 = FileTransferError.INVALID_URL_ERR
 - 3 = FileTransferError.CONNECTION_ERR
 - 4 = FileTransferError.ABORT_ERR
 - 5 = FileTransferError.NOT_MODIFIED_ERR

