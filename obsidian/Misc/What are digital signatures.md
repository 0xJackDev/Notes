
As an aside alot of actual encryption uses symmetric keys because its faster and easier to distribute, but asymmetric encryption is very important for that initial handshake to make sure that the application signer and verifier are the legit people and its the legit application. 

A digital signature proves that the application maker is the legit application maker, then on our end we verify the signature. 

The way this works is with an asymmetric handshake process We tend of this as two people, The person doing the verification and the person doing the signing. 


So the signer will create a digital signature, they will take the application and encrypt it with their private key which will form a signature, They are the only ones who could do that because theyre the only ones with the private key they will then send this signature to the verifier which will then decrypt it with the public key to make sure this matches, Usually though the entire application isnt encrypted as this would be slow and wouldnt really make any sense so instead of encrypted the document this is what we will do.

The signer will take a hash of the original application, encrypt it which will return a signature, then send the signature over to the Application verifier. which will decrypt it with the private key and if the two hashes match then guess what! that is the legit application which hasnt been edited 




Windows uses a process called code signing the verify the authenticity and integrity of applications. Code signed involves digital signatures. 

- **Digital Signature Verification**:
    
    - When an application is signed, it contains a digital signature that includes a certificate from a trusted Certificate Authority (CA).
    - Windows checks the signature to ensure it is valid, confirming that the software comes from a legitimate source and has not been modified.
- **Trusted Certificate Authorities (CAs)**:
    
    - Windows maintains a list of trusted CAs whose certificates are considered trustworthy.
    - If the application's signature comes from a CA on this list, the application is trusted. If not, Windows will display warnings or prevent the application from running, depending on the security settings.
- **Authenticode**:
    
    - Windows uses a technology called Authenticode to verify digital signatures. Authenticode checks the authenticity and integrity of the application by verifying the publisher’s identity and ensuring the application has not been altered.
- **SmartScreen Filter**:
    
    - In addition to signature verification, Windows SmartScreen Filter helps protect against malicious software by checking the application's reputation online.
    - If an application is not commonly downloaded or is unsigned, SmartScreen may warn the user or block the application, even if it's not explicitly malicious.
- **User Account Control (UAC)**:
    
    - UAC provides an extra layer of security by prompting the user when an unsigned or unknown application attempts to make changes to the system.
    - Signed applications can still trigger UAC prompts, but the presence of a valid signature makes it clear that the application is from a trusted source.
- **Driver Signing**:
    
    - For drivers, Windows requires them to be digitally signed, especially in 64-bit versions, to ensure they are safe to install. Unsigned drivers cannot be loaded without specific configurations, which are typically discouraged.
- **Handling Unsigned Applications**:
    
    - If an application is unsigned or has an invalid signature, Windows may block it or display a security warning to the user. The level of enforcement depends on the system's security policies.
- **Certificate Revocation**:
    
    - Windows also checks if a certificate has been revoked by the CA, ensuring that signatures from compromised certificates are not trusted.


### How Authenticode Works:

1. **Digital Signing of the Application**:
    
    - The software publisher signs their application or executable file using a code-signing certificate issued by a trusted Certificate Authority (CA).
    - The signing process creates a digital signature that includes a hash of the file's content and a public key certificate that identifies the publisher.
2. **Hashing the Content**:
    
    - During the signing process, Authenticode generates a cryptographic hash of the application's content. This hash is a unique fingerprint that changes if even a single byte of the application is altered.
    - The hash is then encrypted using the publisher’s private key, creating the digital signature that accompanies the file.
3. **Embedding the Signature**:
    
    - The digital signature is embedded directly into the file along with the certificate from the CA.
    - This certificate includes information about the publisher and the CA, allowing the operating system to verify the identity of the software publisher.
4. **Verification Process**:
    
    - When the user attempts to run the signed application, Windows performs several checks:
        1. **Signature Validation**: Windows decrypts the signature using the publisher’s public key, which is part of the embedded certificate, and compares it to a new hash generated from the current state of the file. If the hashes match, the file has not been tampered with.
        2. **Certificate Chain Verification**: Windows checks the certificate's authenticity by verifying it against the list of trusted root CAs stored in the system. This ensures that the certificate is issued by a trusted CA and not forged.
        3. **Certificate Revocation Check**: Windows checks whether the signing certificate has been revoked by the CA. This check is performed online using a Certificate Revocation List (CRL) or via the Online Certificate Status Protocol (OCSP).
        4. **Time Stamping**: Authenticode supports time stamping, which proves that the file was signed at a time when the certificate was valid, even if the certificate expires later. This is important for preserving the signature’s validity over time.
5. **Trust Decision**:
    
    - If all checks pass, Windows considers the application trusted and allows it to run with the appropriate level of permissions.
    - If any check fails (e.g., the certificate is revoked, expired, or the file has been altered), Windows will warn the user or block the application from running, depending on the system's security policies.
