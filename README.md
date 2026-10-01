# Encrypted access file

[access-key.enc](access-key.enc) is a passphrase-encrypted OpenSSH private key using bcrypt KDF with 100 rounds. The passphrase is supplied separately. No plaintext key or target repository URL is included.

OpenSSH can use the encrypted file directly and prompt for the passphrase. To prepare an unencrypted local copy, copy the file and run ssh-keygen -p -f on the copy interactively; enter the existing passphrase and leave the new passphrase empty. Set file permissions to 600. Never publish the decrypted copy.

Revoke the associated deployment key after use. Deleting this public repository cannot recall downloaded copies.
