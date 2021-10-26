
# Zwave Framework Official Documentation. [![MIT License](https://img.shields.io/apm/l/atomic-design-ui.svg?)](https://github.com/awnishmmg/zwave-framework-3.0/blob/main/LICENSE)
Use This, Documentation to easily build the customised application you would have ever created.
Zwave might be, Lengthy in customisation but provides
quick and easy build and deployement.

## How to Create the Custom Error in Zwave

The Custom 404 Error Page is part of Zwave Configuration.
### Enable Global Error Page
Go to Path, project level 
**project/.htaccess

Copy the Path from ENV_BASE_URL to ErrorDocument
```
 ErrorDocument 404 /myproject/zwave/404.php
 SetEnv ENV_BASE_URL http://localhost:786/myproject/zwave/web-app/
```
    
## How to Add Validation 
```
$data = [];
	$v = new Validator();
	$validator = $v->init();
	$validation = $validator->make(post(),[
		'name'=>'required|alpha',
		'description'=>'required|alpha',
		'rating'=>'required|numeric',
		'duration'=>'required|numeric',
		'instructor'=>'required|numeric',
	]);

	$validation->validate();
	if($validation->fails()){
		$error = $validation->errors();
		$errors = $error->firstOfAll();

	}

```
### How to Perform File Uploading in Zwave using upload.class.php 
Use following step to perform file upload
1. make a folder **resources/uploads
2. autoload the library config/config.php with array value as **upload.class
```
		$banner = $_FILES['banner'];
	if(empty($banner['name'])){
		$errors['banner'] = 'Banner is Required';
	}else{
	$upload = new Upload();
	$upload->set($banner)->max_size(5)->allow_extension('png|jpeg|jpg')->name('file_'.time());
	if($upload->do_upload()){

			$uploaded_file = $upload->file_info();
			prx($uploaded_file);

		}else{
			 $errors['banner'] =  $upload->report();
	}


```
