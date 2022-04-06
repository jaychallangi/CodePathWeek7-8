# Project 7 - WordPress Pentesting

Time spent: 10 hours spent in total

> Objective: Find, analyze, recreate, and document **three vulnerabilities** affecting an old version of WordPress

## Pentesting Report

### 1. Unauthenticated Stored Cross-Site Scripting (XSS)
  - [ ] Summary: When a comment is longer than the MySQL TEXT type size limit of 64 KB, 
        the comment will be truncated resulting in a poorly formed HTML on the page. This allows 
        for stored XSS vulnerabilities to affect wordpress when the comment is loaded.
    - Vulnerability types: XSS
    - Tested in version: 4.2
    - Fixed in version: 4.2.1
  - [ ] GIF Walkthrough: ![Vulnerability 1](https://user-images.githubusercontent.com/72576906/161863165-1e0cff24-d059-495c-b2db-57bcf1c4f17d.gif)
  - [ ] Steps to recreate: First we need to create the comment that is bigger than 64KB. 
        To do this run the code in a64.txt in a python compiler. Then paste the output of the python code 
        in the comment section and post the comment. When the comment is veiwed the XSS will show up.
  - [ ] Affected source code:
    - [Link 1 wp-includes/wp-db.php](https://core.trac.wordpress.org/browser/branches/4.2/src/wp-includes/wp-db.php)
### 2. Authenticated Stored Cross-Site Scripting (XSS)
  - [ ] Summary: HTML containing JavaScript on a WordPress page or post by Contributor or Author level account.
        The malicious JavaScript code will execute when an administrator views the page.
    - Vulnerability types: XSS
    - Tested in version: 4.2
    - Fixed in version: 4.2.3
  - [ ] GIF Walkthrough: ![Vulnerability 2](https://user-images.githubusercontent.com/72576906/161865075-d7cb2f53-e564-442b-8b7a-76c9b9180c74.gif)
  - [ ] Steps to recreate: Enter ```<a href="</a><a title=" onmouseover=alert('test')  ">link</a> ```
        into a page or posting by using the HTML edit mode. When link is clicked on the XSS will show up.
  - [ ] Affected source code:
    - [Link 1 wp-includes/kses.php](https://core.trac.wordpress.org/browser/branches/4.2/src/wp-includes/kses.php)
    - [Link 2 wp-includes/shortcodes.php](https://core.trac.wordpress.org/browser/branches/4.2/src/wp-includes/shortcodes.php)
    - [Link 3 wp-admin/post.php](https://core.trac.wordpress.org/browser/branches/4.2/src/wp-admin/post.php)
### 3. Legacy Theme Preview Cross-Site Scripting (XSS)
  - [ ] Summary: Wordpress themes disallows terms like ```onclick="``` event handlers from being in link tags. 
        However there is a work around for this and thus allowing for an XSS attack.
    - Vulnerability types: XSS
    - Tested in version: 4.2
    - Fixed in version: 4.2.4
  - [ ] GIF Walkthrough: ![Vulnerability 3](https://user-images.githubusercontent.com/72576906/161891173-333bf722-7eda-4bcc-8518-842bb703d816.gif)
  - [ ] Steps to recreate: Create a post with ```<a href='/wp-admin/' title="onclick='" Title='" style="position:absolute;top:0;left:0;width:100%;height:100%;display:block;" onmouseover=alert(1)//'>Test</a>``` 
        as the body.
  - [ ] Affected source code:
    - [Link 1 wp-includes/theme.php](https://core.trac.wordpress.org/browser/branches/4.2/src/wp-includes/theme.php)

## Assets

[a64.txt](https://github.com/jaychallangi/CodePathWeek7-8/files/8423570/a64.txt)



## Resources

- [WordPress Source Browser](https://core.trac.wordpress.org/browser/)
- [WordPress Developer Reference](https://developer.wordpress.org/reference/)
- [Reference for Vulnerability 1](https://klikki.fi/adv/wordpress2.html)
- [Reference for Vulnerability 2](https://klikki.fi/adv/wordpress3.html)
- [Reference for Vulnerability 3](https://blog.sucuri.net/2015/08/persistent-xss-vulnerability-in-wordpress-explained.html)

GIFs created with [ScreenToGif](https://www.screentogif.com/).

## Notes

I had some trouble getting to http://wpdistillery.vm on my host machine as it was not added to my etc/hosts file by vagrant. I needed to manually update the host file to include the ip address and http://wpdistillery.vm.

## License

    Copyright [2022][Jay Challangi]

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
