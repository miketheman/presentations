# Web Flow

!SLIDE

# Web Flow

## How Navigating the Web Works

by: Mike Fiedler

- Twitter: [@mikefiedler](https://twitter.com/mikefiedler)
- Github: [@miketheman](https://github.com/miketheman)

!NOTES

Generate this into HTML format by running:

    $ keydown slides web_flow.md

---
!SLIDE bottom-left

# Question: What happens when you type in `opsschool.org` in your browser and press 'Enter'?

}}} images/questionmarkroad.jpg::milos milosevic::flickr::http://www.flickr.com/photos/21496790@N06/5065834411/

!NOTES

I pose this question to you: (read question).

It feels pretty easy, doesn't it? Let's explore what goes in to browsing the World Wide Web.

* next slide

---
!SLIDE

# Just a moment!

## Let's talk a bit about...

!NOTES

Before we dive into the plumbing of how we surf the web, let's take a moment to talk about some basics.

* next slide

---
!SLIDE bottom-left

# Communication Protocols: [IP]

[IP]: http://en.wikipedia.org/wiki/Internet_Protocol

}}} images/Offutt_Air_Force_Base_operator.jpg::Wikimedia Commons::wikimedia::http://commons.wikimedia.org/wiki/File:Offutt_Air_Force_Base_operator.jpg

!NOTES

Communications protocols are typically formats and rules for systems to exchange messages between them.
One example of a common protocol we use all the time is the Internet Protocol, or IP, which is the primary protocol that is one of the basic foundations of the Internet.
The Internet Protocol is primarily responsible for addressing pieces of data and routing them to their destination.

* next slide

---
!SLIDE bottom-right

# Protocol layering: [HTTP] over [TCP/IP]

[HTTP]: http://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol
[TCP/IP]: http://en.wikipedia.org/wiki/Transmission_Control_Protocol

}}} images/Layers.jpg::John Fowler from Placitas, NM, USA::wikimedia::http://commons.wikimedia.org/wiki/File:Layers_(6925965575).jpg

!NOTES

Protocols can also be layered on top of one another, so that each protocol can concern itself with its own functions.

For instance, the Transmission Control Protocol, or TCP, will use the Internet Protocol to send messages to other computers, and will also ensure that they are delivered, and if not transmit the data again.

The Hypertext Transfer Protocol, or HTTP, is the typical protocol of what we call "The Internet". Even now, most URLs you type into a browser have HTTP in front of them. This is a way for us to tell the browser that we want to use the HTTP protocol when communicating with another server or web site.

HTTP uses TCP, which uses IP, which use hardware or wireless networking communications gear to move data back and forth between your browser and a web server.

* next slide

---
!SLIDE center

# Standards: [IETF], [W3C], [IANA]

[IETF]: http://www.ietf.org/
[W3C]: http://www.w3.org/
[IANA]: http://www.iana.org/

}}} images/MachinedPartsI.jpg::Lyle58::flickr::http://www.flickr.com/photos/lyle58/1074453570/

!NOTES

These protocols have been developed over time, and are now called "standards".
Organizations have worked hard on these and published documents that are used as a standard, or blueprint, for how a protocol should work.
The developers take the standard and implement it, so that when a web server receives a request for a site, the browser will understand the response.

A few of these organizations are:

- The Internet Engineering Task Force
- The World Wide Web Consortium
- Internet Assigned Numbers Authority

There's more, and they all have important jobs in helping shape the Internet to be a better place.
You can visit their sites and read more about them.

* next slide

---
!SLIDE

# Ok, we're back.

!NOTES

So now that we've talked a bit about protocols and standards, let's get back on track of how we navigate the Internet.

* next slide

---
!SLIDE

# Step 1:
# Where to, Boss?

Translate the name provided ([Domain Name]) to an Internet Protocol ([IP]) address using ([DNS]).

[Domain Name]: http://en.wikipedia.org/wiki/Domain_name
[IP]: http://en.wikipedia.org/wiki/Internet_Protocol
[DNS]: http://en.wikipedia.org/wiki/Domain_Name_System

### What does that look like?

!NOTES

First, your computer needs to translate the domain name you typed into an Internet address, also known as an IP address.

It does this by asking another server to look up the address for you, like you would look up a person in the phone book. That server is commonly called a DNS, or Domain Name Services, server.

Your computer has an IP address, which can be seen in a Terminal window, by using the `ifconfig` command on Mac OSX, or `ipconfig` on Windows.

(demonstrate in a terminal window)

We can actually do a DNS lookup ourselves in the Terminal/Command interface using the `host` command.

The term `host` is commonly used to describe any computer connected to the Internet, so your desktop or laptop is a host, and the computer that serves the video you are watching is also a host.

* demonstrate in a terminal window, then advance to next slide

---
!SLIDE

    $ host opsschool.org
    opsschool.org has address 66.228.208.227
    opsschool.org mail is handled by 10 ASPMX3.GOOGLEMAIL.COM.
    opsschool.org mail is handled by 1 ASPMX.L.GOOGLE.COM.
    opsschool.org mail is handled by 5 ALT1.ASPMX.L.GOOGLE.COM.
    opsschool.org mail is handled by 5 ALT2.ASPMX.L.GOOGLE.COM.
    opsschool.org mail is handled by 10 ASPMX2.GOOGLEMAIL.COM.

# So many lines! What do they all mean?

}}} images/PhoneBook.jpg::herzogbr::flickr::http://www.flickr.com/photos/herzogbr/2783660249/

!NOTES

So what we just did was ask our computer to ask the Domain Name Services server for the IP address for the name `opsschool.org`

Line #1 is the command we typed into the command line and pressed enter.
We are asking the computer to do a `host` lookup for us from the DNS server.

Line #2 is the address returned by the DNS Server that we will attempt to connect to.

* explain host aka server
* The remaining addresses are used for email, and we can explain those another time.

* We can also try looking up the same address from specific DNS servers, to see if we get a different response
* using it against 8.8.8.8, 4.2.2.2

Flags to get only the A (host) address: `host -t A opsschool.org`

Other tools: `nslookup`, `dig`

---
!SLIDE

# Are you there, Server?
## It's me, Mike

Send a message from our system to the target

    $ ping opsschool.org

[ICMP]: http://en.wikipedia.org/wiki/Internet_Control_Message_Protocol

!NOTES

ICMP = Internet Control Message Protocol

Results may vary.
Not every server allows ping responses

In our demonstration, we can see a response from the target, so we know that we can each it, but how did we get there?

* next slide

---
!SLIDE

# Directions, please?
## Let's find a route

    $ traceroute opsschool.org

!NOTES

We can use a tool called traceroute to send ping, or ICMP, packets from our system to every router along the way until we find our destination.

This command is called "tracert" on Windows.

This will show us the path our request will take until it reaches the destination server.

Just like with pings, your results may vary, since the path we take on the Internet changes based on where we are, and unless we're sitting next to each other, in the same network, there will probably be differences.

* next slide

---
!SLIDE

# Now you try it!

* What sites do you visit regularly? Find their IP addresses.
* What are some of the other DNS record types you can ask for?
* What interesting things can you find out when tracing a route?


!NOTES

You can pause the video here, try this out some more, and come back when you're ready. We'll be here.

---
!SLIDE

# Let's go!

- Domain name - ✔
- IP Address - ✔
- Route - ✔
- Request - ?

!NOTES
So far, we've used some tools that operate using the DNS, IP, TCP, ICMP protocols.

Now that your browser has translated the domain name to an IP address, and you can see that you have a route to that address, it makes a request using a the HTTP protocol to the destination address, and awaits a response.

---
!SLIDE bottom-left

# Further down the pipes we go!

}}} images/pipes.jpg::alexdecarvalho::flickr::http://www.flickr.com/photos/adc/411821495/

---
!SLIDE

## Step 2: The Request

## "Show me that!"

`GET` request for the root '`/`' page of the site

Uses [HTTP Headers] to send information about the client

Example:

```shell
GET / HTTP/1.1
User-Agent: Mozilla/5.0 ...
Host: opsschool.org
Accept: */*
```

[HTTP Headers]: http://en.wikipedia.org/wiki/List_of_HTTP_header_fields

!NOTES

The request is typically called a `GET` request, as we want to GET the page from the destination server.

A `POST` request will typically be used when submitting a form, or other operations that transfer more data from your browser to the web server.

Our browser formats this request in the Hypertext Transfer Protocol ([HTTP]), and sends it along to the destination server's IP address.

* Request line: `GET / HTTP/1.1`
* User-Agent - identifies the browser/client
* Host - the target site name we want to reach
* Accept - what Content-Types we are willing to receive

---
!SLIDE

## Step 3: The Response

## "Ok, here you go!"

Example:

```shell
HTTP/1.1 200 OK
Server: Apache/2.2.22
Date: Sat, 09 Mar 2013 23:46:34 GMT
Content-Type: text/html
Content-Length: 91
Last-Modified: Fri, 08 Mar 2013 14:04:40 GMT

<!DOCTYPE html>
<html>
<body>
  <h1>My Web Site</h1>
  <p>Hello there!</p>
</body>
</html>
```

!NOTES

informs the client how to handle the content

* Status Code
* Date/Time
* Server
* Content Length & Type
* The Content

---
!SLIDE bottom-right

# How can I do that?

    # Show all options for curl:
    $ curl --help
    # Default behvaior, retreive content:
    $ curl opsschool.org
    # Only retrieve the Response Headers:
    $ curl -I opsschool.org
    # Show both Request & Response Headers, and content:
    $ curl -v opsschool.org

}}} images/Curling.jpg::markjdos::flickr::http://www.flickr.com/photos/markjdos/4532832466/

---
!SLIDE

# Common [Status Codes]

* [200 OK](http://httpcats.herokuapp.com/200) - It's all good.
* [302 Found](http://httpcats.herokuapp.com/302) - Look over there instead
* [404 Not Found](http://httpcats.herokuapp.com/404) - Nothing at this address
* [500 Internal Server Error](http://httpcats.herokuapp.com/500) - General error message

[Status Codes]: http://en.wikipedia.org/wiki/List_of_HTTP_status_codes

---
!SLIDE

## Step 4: Embedded Content

External elements:

* Images [.png, .jpg, .gif ...]
* Stylesheets [.css]
* JavaScript [.js]
* Flash [.swf]
* Streaming video...

```html
<img src="smiley.gif" alt="Smiley face" height="42" width="42">
<link rel="stylesheet" type="text/css" href="css/web_flow.css">
<script type="text/javascript" src="js/web_flow.js"></script>
```

!NOTES

For each object located inside the HTML response, a new call will be made to retrieve that object.
These calls may be made in parallel by the browser to speed things up.

---
!SLIDE

# Step 5:
# Display in browser

!NOTES

The browser will parse the HTML to build the DOM (Document Object Model)

Render the initial content, retrieve embedded content, overlay stylesheets, execute javascript, etc.

---
!SLIDE

# What next?
# Do it again!

---
!SLIDE bottom-left

# Recap

* Step 1: Find where we're going
* Step 2: Request the data
* Step 3: Response with HTML
* Step 4: Gather related content
* Step 5: Browser rendering

!NOTES

So during this video you've learned about some communications protocols and standards, and you've also learned how to use some of these protocols to see the stages involved in navigating web pages in the Internet

---
!SLIDE

# Thanks for surfing!
