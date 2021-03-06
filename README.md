
# Zwave Framework Official Documentation. [![MIT License](https://img.shields.io/apm/l/atomic-design-ui.svg?)](https://github.com/awnishmmg/zwave-framework-3.0/blob/main/LICENSE)
Use This, Documentation to easily build the customised application you would have ever created.
Zwave might be, Lengthy in customisation but provides
quick and easy build and deployement.

## How to Create the Custom Error in Zwave

The Custom 404 Error Page is part of Zwave Configuration.
### Enable Global Error Page
Go to Path, project level project/.htaccess

Copy the Path from ENV_BASE_URL to ErrorDocument
```
 ErrorDocument 404 /myproject/zwave/404.php
 SetEnv ENV_BASE_URL http://localhost:786/myproject/zwave/web-app/
```
Modify the Request Handler in ``` config/request_handler.php ```
Along the Line 64 Replace the Following code in else Block

```

if(function_exists('__error__')){
			return call_user_func_array('__error__',array());
		}else{

			echo("<b> ".get('_method')." url Not Allowed </b><br/>");
			debug_print_backtrace();
			exit;

		}


```
The ``` __error__() ``` will be global function which can modify the response of 404 page not found

### How to make custom helper function ``` show_404 ``` to handle request on 404 request
Goto path web-app/helper/debugger_helper.php Add following code

```
function show_404(){
	load::resource('../404');
}

```
No Go to Any Controller and Add Function at the bottom

```
function __error__(){
	show_404();
}
```
## How to Add Validation 
```
$data = [];
	$v = new Validator();
	$validator = $v->init();
	$validation = $validator->make(post(),[
		'name'=>'required',
		'description'=>'required',
		'rating'=>'required',
		'duration'=>'required',
		'month_duration' =>'required',
		'instructor'=>'required',
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
2. autoload the library config/config.php with array value as upload.class
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
### How to Add Flash Error Messages and Pass on the view 
```
<!-- Adding Error Messages -->

<?php if(count($errors)>0): ?>
<ul style="background-color:white">
<?php foreach($errors as $error): ?>
	<li style="color:Red;font-weight: bold;"><?php echo $error; ?></li>
<?php endforeach; ?>
</ul>
<?php endif; ?>

<!-- Adding Error Messages -->
```
### How to Retain the value of the, Validating Input Fields
Make sure use ``` :id ``` and ``` :name ``` Field on the Input Type Fields 
```
<p> Name: <input type="text" name="name" id="name" value="<?php echo set_value('name',post(),'name'); ?>"/> </p>

```

### How to Manage Redirection State for logged In User
On the Login page Add the following code given below
```
<?php startSection(); ?>
<?php redirect_state('dashboard'); ?>
<!doctype html>
<html lang="en-us">
```

And at the end of the file as the following code
```
</html>
<?php endSection(); ?>
```

### Before Adding Code make a custom function for managing redirection_state(String $redirect_url);
Inside web-app/functions/function.php 
```
//redirection state :: for manging login state of the user dynamically

function redirect_state($redirect_url){
	global $session_key;
	session::start();
	foreach($session_key as $sesskey => $value){
	if(session::get($value)){
		redirect_to($sesskey.'/'.$redirect_url);
		break;
		}
	}
}


```
