gyg-file-controller
===================

File request handler using gyg-framework.


##Installation

1. Create a controller folder in the controllers directory. Name it freely.
2. Download repository and put contents in controller.
1. Whitelist controller.

###Extensions whitelist
Edit the _extensionsWhitelist.php_ file and add the file extensions to whitelist them. Only whitelisted file extensions will be handled by gyg-file-controller. The following is an example from [Playhouse](http://mikael.hernvall.com "Playhouse"):

	return 
	[
		'jpg',
		'png',
		'css',
		'js',
		'less',
	];

##File-handling
The gyg-framework can convert local file paths to URLs, using _path2url_. Converting the path
    
    webroot/controllers/controller/img.jpg
    
assuming _controllersPath_ is set to _webroot/controllers_, will result in
    
    baseUrl/fileController/controller/img.jpg
    
_path2url_ is essentially converting a file path located in a controller's directory into a request URI that points to a path relative to _controllersPath_. Note that 

    baseUrl/fileController/
    
will always be the prefix of the resulting URL. Also, _fileController_ is the user-given name of the file controller.

###Example
####With path2url method
The following is a code excerpt from [Playhouse](http://mikael.hernvall.com "Playhouse").

	// This results in "/file/playhouse/img/faviconMikael.png".
	$renderData['favicon'] = $gyg->path2url(__DIR__ . "/../img/faviconMikael.png");

Note that the file controller is called _file_. The remaining part of the URL is simply the local path to the file relative to the controllers directory.

####Without path2url method
Of course, it is also possible to write out the URL manually. Here's an example how:

	// In controller named "controller", using file controller named "file".
	// Assuming ".png" extension is whitelisted.
	$filePath 	= "/var/www/controllers/controller/img/image.png"
	$fileUrl 		= "/file/controller/img/image.png"
	
Note how _/var/www/controllers_ (the controllers directory) is simply replaced by _/file_.