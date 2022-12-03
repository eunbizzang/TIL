# Encoding: Reversible transformation of data format, used to preserve the usability of data.

Encoding data is a process involving changing data into a new format using a scheme. Encoding is a reversible process and data can be encoded to a new format and decoded to its original format. Encoding typically involves a publicly available scheme that is easily reversed. Encoding data is typically used to ensure the integrity and usability of data and is commonly used when data cannot be transferred in its current format between systems or applications. Encoding is not used to protect or secure data because it is easy to reverse.

An example of encoding is: Base64

# Hashing: A one-way summary of data that cannot be reversed and is used to validate the integrity of data.

What is Hashing?
Hashing is a one-way process where data is transformed into a fixed length alphanumeric string. This string is known as a hash or message digest. A hash cannot be reversed back to the original data because it is a one-way operation. Hashing is commonly used to verify the integrity of data, commonly referred to as a checksum. If two pieces of identical data are hashed using the same hash function, the resulting hash will be identical. If the two pieces of data are different, the resulting hashes will be different and unique.

In addition to verifying the integrity of data, hashing is the recommended data transformation technique in authentication processes for computer systems and applications. It is recommended to never store passwords and instead store only the hash of the “salted password”. A salt is a random string appended to a password that only the authentication process system knows; this guarantees that if two users have the same password the stored hashes are different.

When a user inputs a password to a web application, the password is sent to the web server. The web server then appends the salt to the password and performs a hash function on the password and a salt and compares this output hash with the hash stored in the database for the user. If the hashes match for that user, the user is granted access. Hashing ensures in the event of a breach, or malicious insider the original passwords can never be retrieved. Salting ensures that, if a breach does occur, an attacker cannot determine which users have the same passwords.

An example of a hash function is: SHA512

As an example, say Alice wants to send Bob a file and verify that Bob has the exact same file and that no changes occurred in the transferring process. Alice will email Bob the file along with a hash of the file. After Bob downloads the file, he can verify the file is identical by performing a hash function on the file and verify the resulting hash is the same as Alice provided.

# Encryption: Secure encoding of data used to protect the confidentiality of data.

What is Encryption?
Encryption is the process of securely encoding data in such a way that only authorized users with a key or password can decrypt the data to reveal the original. Encryption is used when data needs to be protected so those without the decryption keys cannot access the original data. When data is sent to a website over HTTPS it is encrypted using the public key type. While encryption does involve encoding data, the two are not interchangeable terms, encryption is always used when referring to data that has been securely encoded. Encoding data is used only when talking about data that is not securely encoded.

There are two basic types of encryption: symmetric key and public key.

In a symmetric key, the same key is used to encrypt and decrypt data, like a password. In public key encryption, one key is used to encrypt data and a different key is used to decrypt the data.

An example of encryption is: AES 256

AES is the Advanced Encryption Standard and is a symmetric key encryption. AES uses a 256-bit key which means there are 2^256, or 1.158x10^77, possible keys that can be used.
