Nginx Server Testing


software Testing GIFs from GIPHY
Below is an example of a postmortem report on an Nginx Server was doing (under pressure)when subjected to a lot of requests(2000 to be specific). A project that was carried out during my study at Alx Africa.

Issue Summary:

We were testing how well our web server setup featuring Nginx was doing under pressure and it turned out it was not doing well: we were getting a HUGE amount of failed requests.

Timeline:

2022–05–02, 6:00 AM EAT: Project release
2022–05–02, 9:00 AM EAT: Begin project. First, head to check for error logs.
2022–05–02, 9:20 AM EAT: Find that error logs are okay, head to /etc/default/Nginx to check the maximum number of file descriptors a process can have.
2022–05–02, 9:35 AM EAT: Found the problem with the high amount of requests made, where our ULIMIT was way below the requests made.
2022–05–02, 9:55 AM EAT: Puppet script running began to increase the limit.
2022–05–02, 10:00 AM EAT: The puppet script finished and the server was able to handle all the requests made. Script pushed to GitHub.
Root Cause:

At 6:00 AM EAT, The project was released to test and strengthen the students debugging knowledge. Now that we are improving our server day by day, by adding different applications and deploying some, There was a need to see how our server will behave if it is subjected to a lot of requests, say 2000 requests with 100 at a time. We are using ApacheBench, Clearly, We can see that 943 requests are FAILED.

Resolution and recovery:

The problem was intentional and an opportunity to strengthen the debugging muscle and a chance to learn should the same issue arise. the system was set to allow few or rather limited requests, and that was found in line 5 of the file /etc/default/Nginx. The line read; ULIMIT="-n 15" The value was increased to ULIMIT="-n 4096" .

Corrective and preventative measures:

In the past few months, we have been learning to debug, The following are crucial:

It is of much essence to do some tests to check whether your server or system is functioning correctly as this allows you to identify the errors early enough before deployment and try to solve them early enough. This will prevent future similar errors occurrence.

In conclusion, testing procedures MUST be more strictly enforced for production environments in the future.


