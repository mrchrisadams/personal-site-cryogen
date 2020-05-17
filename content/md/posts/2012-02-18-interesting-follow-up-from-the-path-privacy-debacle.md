

{:author "admin", :title "Interesting follow up from the Path privacy debacle", :date "2012-02-18 10:44:54", :publish-date "Sat, 18 Feb 2012 10:44:54 +0000"}



<!-- content below -->

After Path were discovered to be uploading their customers address books en-masse from their app, there's been a renewed interest in consumer privacy.

The editor of the Silicon Alley insider issued an terribly written piece efectively saying that everyone was up in arms over nothing at all, but more constructively, Matt Gemmell put out a brilliant piece explaining how this whole scenario could have been avoided, simply by hashing the contents of the address books, and sending that data instead.

This provides all the utility, but avoids stops impinging on customer's privacy, and I if you haven't read it, stop reading here and go read it. 

It's okay, I'll wait.

An other interesting product of this debacle has been the release of a [HashContacts](http://david-smith.org/blog/2012/02/15/hashcontacts-ios-address-book-wrapper/ "HashContacts: an iOS Address Book Wrapper - David Smith"), a free, opensource library to make both asking a user for permission, and hashing an addressbook like this, trivially easy for iOS developers.

> After only 3 hours of effort I wrote a class (available in github) that provides both of these functions in an easily dropped-in fashion.

> Any developer that does not take at least these two trivial steps to protect their customers’ private data is being willfully negligent and should be ashamed

It's available here [on his github account](https://github.com/crossforward/HashedContacts) if you want to use it.

