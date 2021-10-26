
# Zwave Framework Official Documentation. [![MIT License](https://img.shields.io/apm/l/atomic-design-ui.svg?)](https://github.com/awnishmmg/zwave-framework-3.0/blob/main/LICENSE)
Use This, Documentation to easily build the customised application you would have ever created.
Zwave might be, Lengthy in customisation but provides
quick and easy build and deployement.

## How to Create the Custom Error in Zwave

The Custom 404 Error Page is part of Zwave Configuration.
### Enable Global Error Page
Go to Path, project level 
project/.htaccess

Copy the Path from ENV_BASE_URL to ErrorDocument
```
 ErrorDocument 404 /myproject/zwave/404.php
 SetEnv ENV_BASE_URL http://localhost:786/myproject/zwave/web-app/
```
    

