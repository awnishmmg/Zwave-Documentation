
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
