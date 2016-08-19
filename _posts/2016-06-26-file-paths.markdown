---
layout: page
title:  "File Paths"
date:   2016-06-26 08:48:55 -0500
categories: jekyll update
---
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File paths are used to create a link to a different file. Whether you are creating a link that takes the user to a completely different website or linking one page to another in your own website, you must use the correct file path to load your destination file. The browser reads the file path you give it and uses it like directions to then retrieve the correct file.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;HTML supports two types of file paths, absolute and relative. An absolute file path begins with a "/" which basically means to look for the file in reference to the root directory. For all websites the root directory is called the web root. An alternative way of writing an absolute file path would be to include a full URL after the "href=" when defining in a link.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Relative paths give the path to the finle you're looking for starting from a _different_ directory or file. When using a relative file path you don't use the "/" before the file name and extention. If the file you're trying to access is in the same directory as the current file you have open then you would just type the file name or the folder the file is in and then the file name after a "/". You could also use the "./" at the beginning of the file path to say you wanted to start at the current directory. To go up one directory you would use "../" to begin the file path. To move up even more directories you just add another "../". So if you wanted to move up three directories you would start the file path with "../../../".

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;PHP also has the ability to link to your webpages. You can accomplish this by using the include() or require() functions. Both functions basically do the same thing which is link another file to that page basically by inserting it within the HTML script where you call one of the functions. When you call one of these functions in your HTML document you insert the file path for the file you wish to add. You can use either absolute or relative file paths to link your selected file.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;When using relative paths to link pages in your website locally they don't need to match your remote server but when you use absolute paths they do need to match. If they don't then your website won't load correctly. It is important to test your site on a local server if you can before trying to deploy your site on a remote server.