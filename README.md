# Project 7 - WordPress Pentesting

Time spent: **6** hours spent in total

> Objective: Find, analyze, recreate, and document **five vulnerabilities** affecting an old version of WordPress

## Pentesting Report

### 1. CVE-2016-7168 Authenticated Stored XSS Via Image File Name
  - [ ] Summary: 
    - Vulnerability types: XSS (stored), Social Engineering
    - Tested in version: 4.2
    - Fixed in version: 4.6.1
  - [ ] GIF Walkthrough: https://github.com/zipesb/codepath_2022/blob/unit7_wordpress/unit7_vuln1.gif
  - [ ] Steps to recreate: Only tested in Linux. Use social engineering to provide image file to admin that contains malicious HTML/script in the image name and get admin to upload it to the wordpress site. When users view the page containing the uploaded attachment, the HTML/script stored in the image will execute. Possibly restricted to Linux and Mac OS as Windows disallows characters such as "<" in file names.
  - [ ] Example malicious image name: vuln\<img src=a onerror=alert(document.cookie)>.jpg
  - [ ] Affected source code: https://github.com/WordPress/WordPress/commit/c9e60dab176635d4bfaaf431c0ea891e4726d6e0
    - [wpscan page](https://wpscan.com/vulnerability/e84eaf3f-677a-465a-8f96-ea4cf074c980)
### 2. (Required) Vulnerability Name or ID
  - [ ] Summary: 
    - Vulnerability types:
    - Tested in version:
    - Fixed in version: 
  - [ ] GIF Walkthrough: 
  - [ ] Steps to recreate: 
  - [ ] Affected source code:
    - [Link 1](https://core.trac.wordpress.org/browser/tags/version/src/source_file.php)
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
### Vulnerability 1 malicious image name: vuln\<img src=a onerror=alert(document.cookie)>.jpg

## Resources

- [WordPress Source Browser](https://core.trac.wordpress.org/browser/)
- [WordPress Developer Reference](https://developer.wordpress.org/reference/)

GIFs created with [LiceCap](http://www.cockos.com/licecap/).

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
