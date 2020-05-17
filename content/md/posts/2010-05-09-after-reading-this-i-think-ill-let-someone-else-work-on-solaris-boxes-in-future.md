

{:author "admin", :title "After reading this, I think I'll let someone else work on Solaris boxes in future", :date "2010-05-09 13:57:19", :publish-date "Sun, 09 May 2010 13:57:19 +0000"}



<!-- content below -->

I was doing some research on StackOverflow today to find out more about using [Chef-Solo to manage smaller numbers of virtual machines][2] (i.e. less than 5 for example), and I came across this snippet on a [confessional thread about the worst mistakes you've made as a sysadmin][1]:

> I had fun discovering the difference between the linux "killall" command (kills all processes matching the specified name, useful for stopping zombies) and the solaris "killall" command (kills all processes and halts the system, useful for stopping the production server in the middle of peak hours and getting all your co-workers to laugh at you for a week)

Remind me to avoid looking after any Solaris boxes at all costs from now on - if a fairly innocuous Linux command kills an entire system, I shudder to think what other pitfalls and pratfalls lie in wait for a poor sysadmin....

<!-- links -->
[1]: http://serverfault.com/questions/20738/what-do-you-do-to-prevent-stupid-mistakes "What do you do to prevent stupid mistakes? - Server Fault"
[2]: http://serverfault.com/questions/126298/idiomatic-way-to-invoke-chef-solo "Idiomatic way to invoke chef-solo? - Server Fault"

