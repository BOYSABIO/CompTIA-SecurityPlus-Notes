# Non-repudiation
`Non-repudiation` means proving that an action or communication actually occurred and that the person or system that performed it cannot deny doing so later. Verify that information really came from the sender. (Similar to signing a contract but it is in cryptography) 

Simple terms: *You can't say it wasn't you*

In security, we often need to verify:
- Who **sent** a message
- That the message **wasn't altered**
- And that the sender **can't later deny** having sent it  

This protects `integrity` of information and enforces `accountability` between parties (users, systems, organizations).

---

### Example Scenarios
| Scenario | What's Happening | Related Principle |
| --- | --- | --- |
| A user sends an email with a **digital signiture**, confirming it came from them and hasn't changed. | Sender can't deny authorship; reciever can verify authenticity | Non-repudiation |
| A system keeps detailed **audit logs** showing user logins and actions | You can prove who accessed what and when | Non-repudiation |
| An online store requres **cryptographic signing** of transactions | Customer can't later deny making the purchase | Non-repudiation |

---

### How Non-Repudiation Is Achieved
| Method | Description | What It Proves | 
| --- | --- | --- |
| Digital Signatures | Created using asymmetric encryption (private key to sign, public key to verify) | Confirms the sender's identity and message integrity | 
| Public Key Infrastructure (PKI) | Framework for manageing digital certificates and keys | Provides trust and verifiable identity |
| Logging & Auditing | Tracks user activity (who, what, when) | Provides evidence and accountability |
| Time Stamping | Adds proof of *when* an action occurred | Prevents tampering or denial of timing |

Digital signatures = **Cryptographic proof** of `non-repudiation`  
Logs and Timestamps = **Documentary proof** of `non-repudiation`

---

### Non-repudiation vs Integrity
These two are closely related but not the same:
| Concept | Focus | Example |
| --- | --- | --- | 
| Integrity | Ensures data wasn't modified | Hashing verifies a file's contents |
| Non-repudiation | Ensures you can prove **who** did it | Digital signature ties data to the sender | 

Integrity = IT HASN'T CHANGED  
Non-repudiation = WE CAN PROVE WHO DID IT AND THAT IT HASN't CHANGED

Note: *CompTIA loves to ask a question like **Which of the following provides non-repudiation**:*
- `Digital Signatures`
- Hashing or Symmetric encryption

The second option only give **integrity** or **confidentiality** and not proof of identity.

---

### Proof Of Integrity
Any data that we've recieved, we can verify that it is accurate, consistent, and hasn't been changed. In cryptography, we can use something called a `hash`.

You take data and represent it as a short string of text. (It becomes the fingerprint for the specific data.)

If anything changes with that data, there would be a different hash or different fingerprint.

So while this is good at maintaining integrity, it has no way of associating that data to a certian person. You can't verify the **WHO**.


---

### Quick Hashing Example
Hashing turns data into a fixed-length "fingerprint." Even a tiny change completely changes the hash (the avalanche effect).

Example with SHA-256 (values shown truncated):

```text
Text: "hello"  -> SHA-256: 2cf24dba5fb0...938b9824
Text: "Hello"  -> SHA-256: 185f8db32271...26381969
```

- "hello" vs "Hello" differ by one character, yet their hashes are totally different.
- This proves integrity: if the original data changes at all, the hash won't match.

---

### Proof Of Origin
This is a different level of `integrity` in which we are actually able to prove the person behind the data or situation. (Data in cryptography)

By using a digital signature, we are providing non-repudiation which allows not only the sender / reciever to verify who sent it but also anyone else.

Just as someone can use a pen and paper, in cryptography we use a `digital signature`.

In this case you sign with the `private key`:
- The message doesn't need to be encrypted
- Nobody else can sign this (obviously)

Verify the `public key`:
- Any change to the message will invalidate the signature

---

### Digital Signatures (How they work)
Goal: Prove two things at once — the message wasn’t altered (integrity) and it really came from the claimed sender (authenticity), so the sender can’t deny it (non-repudiation).

High-level flow:

1) Hash the message: create a short fingerprint of the data
2) Sign the hash with the sender’s private key: produces the digital signature
3) Send: message + signature (+ often the sender’s public certificate)
4) Verify: receiver hashes the received message and checks the signature using the sender’s public key

If valid, the receiver learns:
- Integrity: the message wasn’t changed (hash matches)
- Authenticity: only the holder of the private key could have created that signature
- Non-repudiation: the sender can’t credibly deny having signed it

Mini example (conceptual):

```text
message = "Pay $100 to Vendor X"
hash = SHA-256(message)
signature = Sign(privateKey_sender, hash)

// Receiver side
hash2 = SHA-256(message)
valid = Verify(publicKey_sender, signature, hash2)
```

Notes:
- Private key stays secret; public key is shareable and used to verify.
- In practice, a certificate (PKI) binds the public key to an identity you trust.
- Digital signatures are not encryption for confidentiality; they prove origin and integrity.

---

### Putting it together: Send/Receive flow (simple mental model)

Sender (Alice):
1) Hash the message (e.g., SHA-256)
2) Sign that hash with Alice’s private key → signature
3) Send: [message, signature, Alice’s public key certificate]

Receiver (Bob):
1) Hash the received message (same hash algorithm)
2) Verify the signature using Alice’s public key (from her certificate)
3) If verification succeeds, Bob knows the message is unmodified and came from Alice.

Key point: The receiver reads the message as data, but does not trust it until the signature verifies. Verification is done immediately upon receipt before treating the message as authentic.

---

### Creating A Digital Signature
On the sender's side:
1. Start with plain text "Send me money".
2. User specifies to sign it digitally
3. Hashing Algorithm creates a hash based on the plain text
4. Once the hash is created, you encrypt the hash with the sender's private key
5. Take the encrypted hash and send it along with the plain text
6. Reciever receives the plain text and attatched to it is the digital signature (Hash + Encrypted signing)

On the receivers side:
1. Reciever receives the plain text and attached digital signature
2. Reciever uses sender's public key which is a key available to ANYONE to examine and decrypt the digital signature using the public key
3. The original hash is left to check if it matches the original plain text that was recieved
4. Plain text is run through a hashing algorithm to do a match check on the hash that was sent from the sender
5. If the hashes match, we know the info is the same and that it had to be sent from the sender.

All of this happens under the hood.

---

## Related Notes
- [[16-Hashing-&-Digital-Signatures]]
- [[11-Public-Key-Infrastructure]]
- [[04-Authentication-Authorization-&-Accounting]]
