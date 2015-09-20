# Usable Authentication

### Golbeck- Psych of why we're bad at choosing passwords
- Pretty much all of them are because of our poor memory, but here's why our choices are bad:
  - We pick easy to guess words (also easy to remember)
  - We reuse passwords from one site to another (super bad if anyone gets the shared password, but super easy for us to remember all of our one password)
  - We share passwords with people. Even if they don't share it on purpose, they might share it
  - We write our passwords down (because our memory sucks)
  - Mnemonics- these can be good, but we typically choose common phrases or words to use the mnemonic on, giving us easy to guess passwords

### Baekdal- The Usability of Passwords
- 5 proven ways to get someone's password:
  - asking
  - guessing
  - brute forcing
  - common word attack
  - dictionary attack
- A password is secure when it is so computationally infeasible for someone to guess it that it won't happen in any interesting amount of time
- Choosing random strings is more secure, but difficult to remember
- There are other ways to choose a secure password:
  - choose uncommon words that have nothing to do with you as a person
  - throw in some symbols as separators
  - use more than one word ie. "this is fun" ← this one is the winner
- There are ways to make this secure from the developer side as well:
  - add a five second delay in between login attempts
  - add a penalty period after every ten (or so) wrong attempts
  - with these a password that would take 2 months to crack at 100 attempts per second would now take 1,889 years to crack

### Two-Factor Authentication
- Adds an extra layer of security by requiring users to enter in their username, password, and one time only passcode that is sent to them via email or text
- This removes a lot of the risk of guessing and sharing passwords
- It also increases the user's perceived level of security
- Unfortunately users report this as being slower, more annoying, less tolerable than single factor authentication
- Tradeoff between usability and security, but this is preferred in some situations where increased security is of higher value than usability

### Biometrics
- Again, there is a tradeoff for each  
  - Voice recognition may be slow or inaccurate if the user is in a noisy environment
    - The user will either need to read words presented to them or remember a pass phrase
  - Facial recognition may be slow or inaccurate if there isn't sufficient light in the environment where the user is trying to gain authentication
  - Fingerprint recognition is typically pretty fast once users are used to the system
  - Any of these could be faked but it would be very difficult
    - The attacker would first need access to the device
    - Then even if the voice could be recorded/picture could be taken/fingerprint could be lifted, it would still require getting those things from the user
    - These attacks are all much more time consuming than writing a script to try hundreds of passwords a second

### Gestures
- These can be keypad gestures
  - User inputs a pattern into a grid (think connecting the dots)
- Or Free Gestures
  - This is more biometric, system analyzes how a user performs a gesture, someone else may draw the same series of lines but it won't be in the same way 
    - This is typically not susceptible to an over the shoulder attack
  - There are also multi-touch gestures which would analyze how a user draws multiple fingers together or draws a line from 2 or three fingers
- Or something in between
  - Users may be asked to interact with an image, connecting certain objects or points in the image
  - This is not biometric (like a free gesture) and **would be** susceptible to an over the shoulder attack
- Benefits:
  - Users enjoy gestures and prefer them to passwords.  This draws a parallel between usability and security
  - Gestures are faster than passwords, and less error prone
 
### Aviv- Smudge Attacks
- There is a lot of information leakage in gesture based authentication from the oils left on the touch screen
- Looking at these smudges is surprisingly effective at reducing the number of possible gesture patterns
  - This was even true when the phone was put in a pocket or rubbed against clothing after validation.  Although some information for swipe directionality was lost.
  - With proper lighting and contrast these patterns were visible even on very dirty phones
- The attacker would still need access to the phone itself to make use of this kind of attack