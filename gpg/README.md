# GPG keys for git use

Keypair geneneration - signing only.

```
$ gpg --full-generate-key --expert
gpg (GnuPG) 2.2.25-unknown; Copyright (C) 2020 Free Software Foundation, Inc.
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Please select what kind of key you want:
   (1) RSA and RSA (default)
   (2) DSA and Elgamal
   (3) DSA (sign only)
   (4) RSA (sign only)
   (7) DSA (set your own capabilities)
   (8) RSA (set your own capabilities)
   (9) ECC and ECC
  (10) ECC (sign only)
  (11) ECC (set your own capabilities)
  (13) Existing key
  (14) Existing key from card
Your selection? 10
Please select which elliptic curve you want:
   (1) Curve 25519
   (3) NIST P-256
   (4) NIST P-384
   (5) NIST P-521
   (9) secp256k1
Your selection? 1
Please specify how long the key should be valid.
         0 = key does not expire
      <n>  = key expires in n days
      <n>w = key expires in n weeks
      <n>m = key expires in n months
      <n>y = key expires in n years
Key is valid for? (0) 0
Key does not expire at all
Is this correct? (y/N) y

GnuPG needs to construct a user ID to identify your key.

Real name: Bart Prokop
Email address: bart@prokop.dev
Comment: Git Signing Key
You selected this USER-ID:
    "Bart Prokop (Git Signing Key) <bart@prokop.dev>"

Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit? O
We need to generate a lot of random bytes. It is a good idea to perform
some other action (type on the keyboard, move the mouse, utilize the
disks) during the prime generation; this gives the random number
generator a better chance to gain enough entropy.
gpg: key 6C899A20D8F9F94F marked as ultimately trusted
gpg: directory '/c/Users/proko/.gnupg/openpgp-revocs.d' created
gpg: revocation certificate stored as '/c/Users/proko/.gnupg/openpgp-revocs.d/BA75E14BB9383D8FF7CD44036C899A20D8F9F94F.rev'
public and secret key created and signed.

pub   ed25519 2021-01-14 [SC]
      BA75E14BB9383D8FF7CD44036C899A20D8F9F94F
uid                      Bart Prokop (Git Signing Key) <bart@prokop.dev>
```

Exporting public key to GitHub:

```
$ gpg --export --armour
-----BEGIN PGP PUBLIC KEY BLOCK-----

mDMEYADYwxYJKwYBBAHaRw8BAQdAkh61GmTgIlXrcYLAc7m0rQd0/+6qSwta4S9r
ivFQ3Sa0L0JhcnQgUHJva29wIChHaXQgU2lnbmluZyBLZXkpIDxiYXJ0QHByb2tv
cC5kZXY+iJAEExYIADgWIQS6deFLuTg9j/fNRANsiZog2Pn5TwUCYADYwwIbAwUL
CQgHAgYVCgkICwIEFgIDAQIeAQIXgAAKCRBsiZog2Pn5T7cWAQC30CBn4obOZ0aA
mmWJ1XDuL0RhS5qHpukXlejr256RdAD/csLg86Hbknbz78Gd6419rU4RJS4oyKQj
qRVmiQolJwE=
=ROjE
-----END PGP PUBLIC KEY BLOCK-----
```

Setting Git to always sign commits

```
$ git config --global user.email "bart@prokop.dev"
$ git config --global user.name "Bart Prokop"
$ git config --global commit.gpgsign true
```

Selecting default private key to use:

```
$ gpg --list-secret-keys --keyid-format LONG
/c/Users/proko/.gnupg/pubring.kbx
---------------------------------
sec   ed25519/6C899A20D8F9F94F 2021-01-14 [SC]
      BA75E14BB9383D8FF7CD44036C899A20D8F9F94F
uid                 [ultimate] Bart Prokop (Git Signing Key) <bart@prokop.dev>

$ git config --global user.signingkey 6C899A20D8F9F94F
```
