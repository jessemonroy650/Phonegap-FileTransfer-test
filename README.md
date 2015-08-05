# Phonegap-FileTransfer-test
a simple test of Phonegaps's FileTransfer API

Documentation source: [cordova-plugin-file-transfer](https://github.com/apache/cordova-plugin-file-transfer/blob/16249c2f7ac53cb593e11eeae180066a88a28271/doc/index.md) <br />
The source is poorly written & incomplete.

##Properties##

* onprogress

*`onprogress` gets called as the file transfer progresses. The parameters sent to it are not well documented. <br />The parameters are:
 - e.lengthComputable - (boolean) determines if the length of the file is computable
 - e.loaded - (long) running byte count of bytes transfered
 - e.total - (long) total number of bytes to be transfered

NOTES: From example code in documentation, and [src/android/FileProgressResult.java](https://github.com/apache/cordova-plugin-file-transfer/blob/16249c2f7ac53cb593e11eeae180066a88a28271/src/android/FileProgressResult.java)

##Methods##

* upload
* download
* abort

##Parameters##

###upload (method)###

* fileURL
* server
* successCallback
* errorCallback
* options
* trustAllHosts

###download (method)###

* source
* target
* successCallback
* errorCallback
* trustAllHosts
* options

##abort (method)###


###FileUploadResult (object)###


* bytesSent: The number of bytes sent to the server as part of the upload. (long)
* responseCode: The HTTP response code returned by the server. (long)
* response: The HTTP response returned by the server. (DOMString)
* headers: The HTTP response headers by the server. Currently supported on iOS only. (Object)
 * iOS does not support responseCode or bytesSent.


###FILES###

* index.html - main program

* js/fastclick.js - remove 300ms delay form Android
* js/zepto-1.1.6.js - jquery clone
* js/parse-1.3.2.js - parse.com service
