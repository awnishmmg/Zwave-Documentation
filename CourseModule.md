
# Working with Course Module in LMS Project inside admin
## Step 1:
### Make sure your ```dbadmin``` is running if not use the command to open dbadmin
```
php zwave serve launch::dbadmin

``` 
Login to Adminer Database connect with your credentails
Make sure you select the database ```lms``` in the database
Goto SQL Command and
Now Execute the Following Query to make ```tbl_course```

### The Standard Query of ```tbl_course```

```
CREATE TABLE `tbl_course` (
  `id` int(11) NOT NULL AUTO_INCREMENT PRIMARY KEY,
  `course_name` varchar(255) NOT NULL,
  `duration_hr` int(11) NOT NULL,
  `duration_month` int(11) NOT NULL,
  `course_rating` varchar(10) NOT NULL,
  `course_description` text NOT NULL,
  `user_id` int(11) NOT NULL,
  `is_banner_added` int(11) NULL,
  `banner_path` varchar(255) NULL,
  `is_syllabus_added` int(11) NULL,
  `syllabus_path` varchar(255) NULL,
  `created_by` int(11) NULL,
  `updated_by` int(11) NULL,
  `deleted_by` int(11) NULL,
  `created_at` varchar(255) NULL,
  `updated_at` varchar(255) NULL,
  `deleted_at` varchar(255) NULL,
  `status` varchar(255) NULL
);

```
## Step 2:
### How to create ``` course_model ``` goto ``` web-app/model/admin/ ``` create a file ```Course_model.php ``` and write the following code.

Make sure File name and class name should be same , also make sure the first letter of File and class name should be capital.

```
<?php

class Course_model{

  public function add_course($formdata){

    global $chain;
    $chain = false;
    if(insertat('tbl_course',$formdata)){
      return true;
    }else{
      return false;
    }
  }
}



?>
```

## Step 3:
### Create the ``` now() ``` function inside ``` timestamp.php ``` which is inside path

``` web-app/functions/timestamp.php ``` 
Add the following line of code on ``` line no: 13 ```

```
function now(){
  return date('Y-m-d H:i:s');
}

```
Note: This ``` now() ``` will be used for, Adding timestamp (date + time) to the field.

## Step 4: 
### In Order to get Any Information from session we always have to use this code,

```
      $session_data = session::get('session_data');
      prx($session_data);

```

## Step 5:
### Now goto the ``` web-app/admin/CourseController.php ``` Add the following code in else block after if($validation->fails()){ } Block

```
    //check for validation
    $validation->validate();
    //check if validation fails
    if($validation->fails()){
      $error = $validation->errors(); //get all the validation
      $errors = $error->firstOfAll(); // and first of all show it 
      $data['errors'] = $errors;
      $data['users'] = $users;
      load::resource('admin/views/course/add',$data);
    }else{

      //form submitted
      load::model('admin/Course'); #load 
      $course_model = new Course_model(); #Object

      $session_data = session::get('session_data');
      $created_by = $session_data['user_id'];

      $formdata = [
        'course_name'=>post('course_name'), //Add Your Column names
        'duration_hr'=>post('duration_hr'), //Add your fields names
        'duration_month'=>post('duration_month'),
        'course_rating'=>post('course_rating'),
        'course_description'=>post('course_description'),
        'user_id'=>post('instructor'),
        'is_banner_added'=>'0',
        'is_syllabus_added'=>'0',
        'created_by'=>$created_by, //get it from session
        'created_at'=>now(), // get from timestamp.php
        'status'=>'active', // set active status

      ];

      //if it return true set flash data with success or else
      // with danger and redirect_to back to from
      if($course_model->add_course($formdata)){
        set_flashData('message','Course Added Success','success');
        return redirect_to('admin/course/create');
      }else{
        set_flashData('message','OOps Cannot Added','danger');
        return redirect_to('admin/course/create');

      }
    }


```
