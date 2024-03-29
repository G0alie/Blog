<html>
<h1>Hack The Box Legacy writeup</h1>

Legacy is one of the easier retired machines hosted on Hack The Box, which is why I selected it as my first writeup.<br><br>

First we'll run an nmap scan on the target.
  <blockquote>nmap -A -T4 -p- -oN legacy.txt 10.10.10.4</blockquote
<ul> 
    <li>-A : For for version information, script scanning, and OS detection.  This shouldn't be used in real testing scenarios without permission because the script scanning portion can be intrusive and cause some damage.</li> 
    <li>-T4 : To speed the scan up in aggressive mode.  In real testing scenarios, this will probably be picked up by the IDS system.</li> 
    <li>-oN legacy.txt : This will write the results to a file named legacy.txt</li> 

</ul>

<pre><img src="https://i.postimg.cc/T2C4JhvR/nmap-legacy.png"/></pre>

Running a searchsploit on smb shows us some remote code execution vulnerabilities.  The ones that caught my attention was ms_017_10 EternalBlue.

Since this is on metasploit, we will launch msfconsole and search for smb.  Using the EternalBlue exploit does not get us a shell, but there was another ms_017_10 remote code execution exploit a few lines down called EternalRomance, so lets try that out.<br><br>
<pre><img src="https://i.postimg.cc/ZRYcMk1G/search.png" alt="search in msfconsole"/></pre>

We'll set the RHOSTS to the target IP, 10.10.10.4, and run the exploit. 

<pre><img src="https://i.postimg.cc/sXQF10cZ/msfconsole.png" alt="msfconsole"/></pre>

Now we have a meterpreter shell.  Using the pwd command, we see we are in the WINDOWS folder.  The user flag will be on the desktop, so A little bit of googling will show you where the Desktop file is located in windows XP systems.  We cd back to the parent directory and go to the Documents and Settings folder.  A user named John is listed, and on his desktop we find the user.txt flag.

This box does not require any extra steps for privelege escalation.  We can just navigate back the the Documents and Settings directory, and cd to the Administrator folder. On the Admin's desktop lies the root.txt flag. 
</html>
