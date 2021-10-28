
# Working with Course Module in LMS Project inside admin
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
