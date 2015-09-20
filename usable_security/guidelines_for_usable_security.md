# Guidelines for Usable Security
- Both security and usability should be features that are implemented throughout the design process, not implemented after the fact
- Usability and Security shouldn't be at odds with one another, if they are carefully planed out and implemented throughtout an iterative design process they can go hand in hand 

### Permission vs Authority
- permissions are settings within a system that say who can access a file
- authority says who has the power to access something (this is independent of permissions on a system)
- someone can have authority to access a file without having permission within the file's original system
- authority is access to resources or information that the user controls

### Guidelines for authority
- match the easiest way to do a task with the least granting of authority
  - what are typical tasks?
  - what is the easiest way for the user to accomplish each task? this is the way that they'll choose
  - what authority is granted to software and other people when the user chooses this route?
  - how can the safest way of accomplishing this task be made easier?
  - how can the easiest way of accomplishing this task be made safer?
- the natural easy way a user could do a task should also be the most secure
- think the 'sign in with facebook/google/etc' buttons
  - this is typically much easier, but is the user giving up too much authority?  
  - there is a lot of extra public info that we may have on facebook but that we dont actually want to share (friends, gender, age)
- a system should be given the minimum amount of information necessary to proceed
- think of alcoholic sites that request your birthday, they don't actually need your full birthday (just whether or not you're over 21)
  - with your exact birthday and IP address location, these sites could actually figure out who you are (about 85% of the time from a birthday, zipcode, and gender)
- Sometimes the user might not understand what they've granted authority to 
- example given is that of the post readers connected from facebook.  Just clicking okay, read article, users reading information was getting shared with their friends
- you should always offer *simple* ways to reduce the permissions granted if a user wants to rescind a decision
- make **sure** the user consents to any access they allow and know that they are doing it 

### Typical Problems with Authorities
- Some software may have the authority to execute other programs
- This becomes a problem when those launched files launch other files
- The user needs to know whether or not software will automatically execute a file
- The user should have this option and it should be easy for them to know at any time what authority they have granted
- The user also needs to know what authority they have, so they have a better idea of what they've delegated
  - Ex. paypal actually still has authority over money while the money is in your paypal account
- You need to make sure the users trust the software that will be acting on their behalf when delegating authority
- Make it clear in the interface who the user is interacting with
  - Browser prompts for passwords with the box hovering over an area above the page itself, this couldn't be faked with css from the typical window

### Designing Interface Features for Security
- think of mac's `get info` and `change permission` at the bottom, or changing permissions for a google doc.  these are good
- `chmod`ing would not work for the typical user
- only expose to the user what they really need to have control over
  - users don't need to see everything associated with a file download, but they shouldn't click a file and have it opened and installed on their computer.
- mac apps are seen as nothing more than an icon, although they're actually a directory. typical user's won't need to see anything other than the icon
- it should be as easy as possible for the user to tell whats good (your software) and what could be malicious
- think PayPal getting spoofed by a site that uses a capital I rather than an l at the end. 
  - you should create an environment where it would be very easy for your users to notice a difference like this

### Case Study: Phishing Site
- Google will disable malicious links even if you choose to ignore their warnings
- This is typically good, but could have false positives
  - In this case it might be a good idea to give some power to the users, so you don't prevent them from navigating to a safe site that they want to go to
  - Prompt users to trust sites that they haven't trusted yet, this can be done in their normal workflow and draw their attention to sites that could be harmful
  
