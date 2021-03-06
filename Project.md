
# Following the following code to Work with student module
## Step 1:
### Change the Links of the navigation inside ``` web-app/view/layout/common/nav_view.php ```

Copy paste the code or type according to your choice.

```

<div id="menu">
<ul>
	<li><a href="<?php echo base_url('home.php'); ?>">Home</a></li>
	<li><a href="<?php echo base_url('about.php'); ?>">About</a></li>

	<li><a href="<?php echo base_url('student/enroll'); ?>">Register</a></li>
	
	<li><a href="<?php echo base_url('contact.php'); ?>">Contact</a></li>
</ul>
</div>

```
## step 2:
### Make the following change in ``` web-app/config/session.php ```
Add the following piece of code
```
#page where session will not be created
$session_not_allowed[] = 'login'; 
$session_not_allowed[] = 'home.php'; 
$session_not_allowed[] = 'about.php'; 
$session_not_allowed[] = 'contact.php'; 
$session_not_allowed[] = 'student';  //This is change we made note that, any url after student will not require session

```
## Step 3:
### No Url will be loaded unless and until mvc Rewrite Rules are added in .htaccess file

Find the File ``` web-app/.htaccess ```

Add the Following lines of code.

```
#student Enrollment Controller
RewriteRule ^(student/enroll)/([a-zA-Z0-9\-]+)/([a-zA-Z0-9\-/]+)$ register.php?_method=$2&_values=$3 [L,QSA] 
RewriteRule ^(student/enroll)/([a-zA-Z0-9\-]+)$ register.php?_method=$2 [L,QSA] 
RewriteRule ^(student/enroll)$ register.php [L,QSA]

```

## Step 4:
### In Order to work in same pattern, that you have done in admin or will require, mvc approach that you already know goto path ``` web-app/view/ ```
make a folder ``` views ``` parallel to layout and errors Please Refer
to project structure

### web-app
###   |------>view
###             |----->errors
###             |----->layout    
###             |----->views [MAKE YOUR FOLDER HERE]

Create some file called as ``` enroll_view.php ``` please make sure you add ``` _view.php ``` as extension.

Goto file enroll_view.php as following code

```
<h1>Student Register Here</h1>
<hr>
<form>
	<!-- Make your student form here same as course controller -->

</form>

```

## Step5:
### Now we ready to code in mvc framework goto controller ``` web-app/register.php ```
Add the following code

```
<?php 

// Student Enrollement Controller

Request::method('',function(){
	load::view('views/enroll');
});

Request::method('create',function(){
	prx('Method Created');
});


function __error__(){
	show_404();
}


```

## Step6:
### Now last step is Add Routes for the controller ``` web-app/config/routes.php ```

Copy paste or Add the Following Code.

```

$routes['admin:DashboardController'] = array('main','logout');
$routes['admin:ManageUserController'] = array('add-new','add-new-bdagent','user','bds','delete','bds-delete');
$routes['admin:DepartmentController'] = array('manage','add');
$routes['admin:ChangeLoginController'] = array('user','admin');
$routes['admin:ContactsController'] = array('add','manage','create','delete');
$routes['admin:CourseController'] = array('manage','create','save');

//  This Code is Added for the Student
$routes['student:register'] = array('','create');

```


### Goto Url:
```
 http://localhost:<port-no>/your-project/web-app/student/enroll
```


