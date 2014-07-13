---
layout: post
title:  "Apis for SRM's ERP"
date:   2012-07-15 14:49:07
categories: jekyll update
---



I recently read about the dude who scraped the entire ICSE results, that got me going. I had a crack at this a several months ago, Maybe I wasn't thinking clearly at the time. Scraping data from any site is actually pretty simple, You just need to understand what's going on. I started off by playing a litte with [V8](https://code.google.com/p/v8/)(A thing of beauty). I was trying to get what I wanted using the defined html selectors, I didn't know Jquery at the time, so I wrote a little JS code. This simply, Picks out our needle from the hay stack.
<img src="https://db.tt/CS0fuYAs" />

I wasn't really going anywhere with this. You'll need to login in with your register number and password, for this script to run from your browser. The ultimate aim was to make a AJAX call to my server and dump all the data there. Automating Logging-in seemed to be the problem.

I came up with a partial solution which involved, storing register numbers and passwords in my database and sending them to evarsity via a HTTP GET call, like I've shown below

{% highlight javascript %}  
getStudentDetails(1);
setTimeout(function(){
var string=''; 
var table = document.getElementsByTagName('table'); 
var tr =table[1].getElementsByTagName('tr'); 
var td =tr[1].getElementsByTagName('td'); 
var name=td[1].innerhtml; 
for(var i=1; i<=10;i++) 
{ 
  var td =tr[i].getElementsByTagName('td'); 
  string= string + td[1].innerHTML+ '|'; 
}
var td =tr[11].getElementsByTagName('td');
var x= td[1].getElementsByTagName('input'); 
string= string + x[0].value + '|';
for(i=12; i<=15;i++) 
{ 
  var td =tr[i].getElementsByTagName('td'); 
  string= string + td[1].innerHTML+ '|'; 
} 
alert(string);
},5000);
{% endhighlight %}


I was unaware of concepts like PHP cURL at the time so, I popped this URL in a new window, and set up [Greese Monkey](https://addons.mozilla.org/en-US/firefox/addon/greasemonkey/) to parse and stash. The major issue with this predominantly Javascript Solution was that, It would run only on my PC and that too only on Mozilla and It was pretty much manual.

* * *

Over the last year, My knowledge about web technology has grown in leaps and bounds. With what little I know now, the problem at hand seemed very simple. Why not pick an alternative apporach? Then I realized the power of cURL. How can you emulate a browser action? That was the question. Well actually, you can. cURL is Kick-Ass. Too bad it took so long for it to walk into my life. Lot of good things came about after un-installing windows.


I found a [php-cURL-class](https://github.com/lepunk/curl.class.php/blob/master/curl.class.php) somewhere on gitHub. Works perfectly, you just need to adjust permission on that directory in Linux, no big deal. Then you're set.

Think about it, What happens when you type in the Register Number, Password and click on login. The Contents from the text box are sent to a new URL through a simple HTTP GET/POST. cURL helps you automate this process. You can do it like this.

{% highlight php %}
$cc = new cURL();
$data = $cc->get('evarsity.srmuniv.ac.in/srmswi/usermanager/
youLogin.jsp?txtSN='1081020035&txtPD=myPassword&txtPA=1');
// or you can even POST
$data = $cc->post('evarsity.srmuniv.ac.in/srmswi/usermanager/
youLogin.jsp',"txtSN=1081020035&txtPD=myPassword&txtPA=1");
echo $data;
{% endhighlight %}

[Evarsity.Srmuniv.ac.in](http://api-srmapi.rhcloud.com/magic.php#) uses a HTTP POST to transfer auth data, but the thing with JSP is it doesn't differentiate between a HTTP GET and a HTTP POST. Both methods work, unlike in PHP where you're likely to face an error. Weird. I'm still not able to figure out a reason to substantiate this behavior. As I said, Weird.

* * *

Now that we're in, we need to scrape what we need. Remeber that basic information that shows up after logging into ERP, lets first scrape that. Again with the power of the internet I found another useful tool a [php DOM parser](http://simplehtmldom.sourceforge.net/). cURL returns only hyper-text. So using this parser we can take what we need, Just like that. So for example, I need to get what's there in the 5th cell in 3rd row of the 2nd table in the page. I do it like this.

{% highlight php %}
$html = str_get_html($data);  // $date is the result of cURL 
$table = $html->find('table');
$tr = $table[1]->find('tr');  // $table[1] is the 2nd table
$td = $tr[2]->find('td');  // $tr[2] is the 3rd row
{% endhighlight %}

Getting the Attd information isn't as straight forward. When you click on attendence, some AJAX stuff happens and the Attd is fetched from. 

{% highlight php %}
http://evarsity.srmuniv.ac.in/srmswi/resource/StudentDetailsResources.jsp?resourceid=7
{% endhighlight %}

If you do a cURL to this url without logging in, you'll get a Apache Error. This is the important part, How is the server knowing wether I've logged in or not. I'm not specifying this information anywhere in the URL. It uses a JSESSIONID cookie,which is injected into the browser on login. You can see the value of this by typing `document.cookie` in your javascript console. But you don't have to worry about this. cURL takes care of everything. It creates a text file cookies.txt which stores the JSESSIONID value after every successful login. So cURL to the url mentioned, parse the HTML and you have your attendance information.

Now that we have what we need, Now we do with it is up to us. I've written a set of APIs which are hosted on [RhCloud](https://openshift.redhat.com/).

* * *

<img src="https://db.tt/zYdXGlu6" /><br />

What will happen if the regno/password comination is wrong. How can we check this? There are only two possibilites, If the login is valid and if it isn't. We can check this by clues within the hyper-text. So if login is valid, the success page (i.e) your home page will have the details of the logged in student and it it's in valid it will have an error string "Login failed, Username and password do not match". We can look for such clues in the hyper-text to verify wether we have logged in properly. Checking for only one string may not be advisable, if the developers end up changing the hypertext a little, We are screwed! It's better we check for multiple cues.

* * *

[Github](https://github.com/nithinkrishna/srmapi).[Website](http://api-srmapi.rhcloud.com).[Screen Shot](https://db.tt/HsDUxsWr)