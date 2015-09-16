# Confidentiality
- Knowing that only you and your target see the data you wish to communicate
- goal is just to prevent unauthorized viewing of private information
- The bad guy (not bob or alice) is trying to see data as it moves across the internet

### Encryption
- Many different ways to encrypt text
- One of the early and most basic ways was the ceasar cipher, all letters in a message would be shifted a certain number of letters to form the desired word
- for the strings "upbtu" and "Uryyb, zl anzr vf Puhpx naq V arrq zbarl naq n wrg":
```rb
alph = ('a'..'z').to_a
str = YOUR_CIPHERTEXT

26.times do |r|
  rotated = alph.rotate(r)
  mapped = str.downcase.split('').map do |chr| 
    if chr =~ /[a-z]/
      chr_idx = alph.index(chr)
      chr = rotated[chr_idx]
    else
      chr
    end
  end.join('')

  puts mapped
end
## => shift of one yields "toast"
## => yields "hello, my name is chuck and i need money and a jet"
```
- notice that you can see I and/or more common letters/words and guess what the shift is

# Integrity
- A cryptographic hash function is a function that takes an arbitrary block of data and returns a fixed-size string (the cryptographic hash value), such that any change to the data or message will change the hash value.
- This is often referred to as the digest

#### A good hash function:
- Takes a message or block of data and returns a digest that is fixed size no matter what
- Any tiny change to the original message will change the hash dramatically
- Doesn't allow collisions (ie the same signature being used to sign two different messages)
- SHA1 has been proven to have shortcomings, SHA256 is favored

#### Applications for hashes
##### Passwords
  - Unforgivable to store a password in a database
  - If anyone uses the same password for more than one thing, finding one password could ruin all of them
  - Instead you hash the password and store that, then hash the password the user enters and check it against the stored digest
  - Digests should be one way, you can't derive the password from the digest

##### Digital Signatures
  - Simple Message Signing
    - Shared secret is shared securely somehow
    - before sending the message you concatenate the secret to the message
    - compute the SHA digest of the concatenation
    - send this whole thing across the insecure network
  - Recieving that message
    - Recieve the message plus the digest
    - remove digest and add the secret to it
    - compute the SHA digest for the message and the secret
    - compare the computed digest to the received digest

## Public Key Encryption
- Proposed by Whitfield, Diffie, and Hellman in 1976
- Rely on two mathematically related keys, this is an asymmetric cryptosystem 
- One key is public, this is openly revealed, second is private
- Message encrypted with one key can only be decrypted with the other
  - it is computationally infeasible (not impossible) to recover one key from the other
- Generating these public/private key pairs
  - Choose 2 very large random prime numbers
  - Multiply them
  - Compute public and private keys from the number
  - Easy to pick these, but extremely expensive to figure out the two factors from the product
- Steps:
  - Amazon sends you their public key as part of the beginning of establishing the secure connection
  - You encrypt using that public key and send the ciphertext back
  - Amazon uses their private key to decrypt, you don't need to know how to decrypt your own message, so private key never has to be revealed to anyone but amazon

#### Transport Layer Security
- This is a mini layer that sits on top of the socket, in between the application and transport layers
- It encrypts your plain text and decrypts ciphertext before returning it to you
- This way all of the data inside of the insecure internet is ciphertext
- You get to be blissfully unaware that the encryption/decryption is ever even happening
- Packet sniffers only ever see ciphertext
- This is known as Transport Layer Security (TLS, HTTPS)
  - Used to be called SSL
  - Passwords/private data/etc should never be typed without https in the URL
- Greatest danger to losing data is now:
  - Virus on your computer collecting your key strokes
  - Browser isn't actualy talking to the real Amazon

## Certificate Authorities
- Public keys must be signed, way of letting you and your browser know that you're talking to who you think you're talking to 
- A Certificate Authority is an entity that issues digital certificates.
  - Certifies the ownership of a public key to the subject of the certificate.
  - They are a trusted third party
- Digital Certificate
  - electronic document which uses a digital signature to bind a public key with an identity
  - Verifies the ownership of the public key to prevent redirection (ie you interacting with an evil version of Amazon)
- These authorities can also use public/private keys for signing the certificate
- So amazon generates public/private key pair
  - Sends it to verisign
  - Verisign signs it with their public key and says its really from amazon, sends it back signed
  - Amazon has signed public key, sends it to you (you already had verisign public key as these often come with laptops, but you can also go verify this online)
  - You can check to see that the public key came from amazon, signed with verisign
  - When you know that it is you can send your credit card data encrypted with the public key back to amazon
  - Amazon decrypts and carries out the transaction
  - Someone could be watching for every single step and wouldn't be able to do anything
  
