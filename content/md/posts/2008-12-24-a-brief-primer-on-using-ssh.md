

{:author "admin", :title "A brief primer on using ssh  ", :date "2008-12-24 15:15:57", :publish-date "Wed, 24 Dec 2008 15:15:57 +0000"}



<!-- content below -->

<em>I keep forgetting how to do this, so I'm writing this here for future reference.</em>

This year, as I use web app frameworks like Django or Rails more and more, I've increasingly been using the command line instead of tools like Transmit for making changes to sites and web apps. This works fine locally, but when you start using remote servers, typing passwords all day gets old quickly.

This is where logging into servers using ssh keys comes in. This a very high level abstraction, and isn't that accurate technically, I found it easiest to think of this process as three separate steps:

1) Generate a lock and key
2) Put the lock on the server.
3) Use the key to get into the server.
<h3>Generate the lock and key - generate your key pair</h3>
Essentially what you do is generate a private/public key pair, and put the public part of the key onto the remote server. The server can then check your the public key you gave it against the private key on your laptop, and if they 'fit', it's pretty sure you are who you say you are.

First , you generate the key pair, using the program ssh-keygen, and telling it to use the encryption type 'rsa':
<pre class="literal-block">ssh-keygen -t rsa</pre>
The two common options here are to use -rsa type encryption, or -dsa encryption. <cite><a title="DSA authentication" href="http://en.wikipedia.org/wiki/Digital_Signature_Algorithm">DSA</a></cite> stands for Digital Signature Algorithm, whereas <cite><a title="RSA  authentication" href="http://en.wikipedia.org/wiki/RSA">RSA</a></cite> is named after the three inventors of the algorithm; Ron Rivest, Adi Shamir and Leonard Adleman.

I haven't found any real difference that affects my experience of ssh as a developer, but the gist I get from skimming the newsgroups is that DSA is a slightly faster encryption algorithm than RSA, but also slightly less difficult to (eventually) crack.

My understanding earlier was that DSA was the more 'free' encryption method, as RSA was under patent initially, but a quick check on wikipedia tells us that RSA released to the public domain in the year 2000, so for most of us non-crypto profs, there's almost nothing in choosing between the two now.

Running this command will create a public/private key pair, usually put in an invisible directory called <cite>.ssh</cite>, and they should look like this if you peep inside the <cite>~/.ssh</cite> directory:

<dl class="docutils"><dt><cite>id_rsa</cite></dt><dd>Your private key, which you keep on your computer. This shouldn't be shared with anyone, and though it's not totally accurate, I like to think of ssh key pairs in similar terms to locks and keys. In this case we can think of this as the front door key.</dd><dt><cite>id_rsa.pub</cite></dt><dd>your public key which you put on the remote server, specifically in a file called authorized_keys. You can think of this as the 'lock' that you would put the id_rsa private key into.</dd></dl>
<h3>Put your the lock (the public key) on the remote server</h3>
You next need to put the public key into the hidden <cite>~/.ssh</cite> directory, appending the public key to a file called <cite>authorized_keys</cite> on the remote server. When you next try to ssh into your server, you'll end up combining your private key on your computer, with the public key on the server, to give a fairly strong claim to you being who you say you are.

Once you've copied it onto your server, which you can do using an <cite>sftp</cite> client, or simply using <cite>scp</cite>,You need to make the server aware of the public key by writing it to a text file called authorized_keys. A simple way to do this is to use a command called <cite>cat</cite> (think con<strong>cat</strong>enate):
<pre>cat .id_rsa.pub &gt;&gt; ./ssh/authorized_keys</pre>
This takes the contents of your public key, and writes it to the end of the authorized keys file.

To continue the clumsy lock and key analogy, this is like fitting the front door with the new lock that responds only to your private key.

Exit the <cite>ssh</cite> session, and then try logging in once more..
<h3>Log in</h3>
Et voila! You should now have passwordless log-in to a server setup from your computer to a remote server now. You can use a variant of this setup to create secure automated backups from one server to another, and to set up other dull tasks that are best automated.

It doesn't stop here though - you can ramp up security here by limiting what tasks a script, or person logging in using ssh can do on a server, and you can add extra layers of security to make key pairs AND passwords needed for certain accounts, or certain actions, or set up elaborate daisy chain sequences where an action on one computer sets of a series of other automated tasks on other computers around the web that you'd previously have to do by yourself. But that's for a future post.

<em>Common gotchas here</em>

I've lost a depressing amount of time trying to setup ssh keys for passwordless login, before realising that I needed to fiddle with file permissions on the relevant files.
If you're still being challenged for a password when you're signing, check that you have the permissions setup properly on your server. You need to be the only person able to alter the <cite>authorized_keys file</cite>, on the remote server, and you can do this with the tool <cite>chmod</cite>, like so:
<pre class="literal-block">chmod 600 ~/.ssh/authorized_keys</pre>
This gives you read and write access to the <cite>authorized_keys</cite> file (the 6), but removes anyone else's access to it (the second and third 0's). Which makes sense really - for security you want to be the only person who can decide who is allowed to add authorised user's public keys.

You also need to check that your hidden <cite>~/.ssh</cite> has similar permissions: you want to be the only person who can edit the directory, so make sure this is reflected in the permissions. You need to set chmod to 700:
<pre class="literal-block">chmod 700 ~/.ssh/</pre>
Once again, this grants access only to you, and no one else.
<h3>Isn't logging into a server without a password a horrifically bad idea security wise? What if someone steals your laptop?</h3>
If you lose the keys to your house, it's a good idea to change the locks, so people with those keys can't get in. Likewise, if you lose your computer, the equivalent action to changing your locks would be removing that laptop's public key from your server's list of authorised keys.

I've borrowed heavily from <a title="James Gardner - ssh primer" href="http://jimmyg.org/2008/07/26/beginners-guide-to-ssh-keys-with-ssh2/">James Gardner's own writing about ssh</a>, so if you're interested in learning more, he's written quite lucidly and at length about them on his own blog.

