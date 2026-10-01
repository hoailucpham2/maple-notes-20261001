# Delivery

Download [delivery.zip](delivery.zip). Its contents are protected with a separately provided passphrase using WinZip AES-256 encryption. Internal file names are visible, but the instructions and key contents require the passphrase.

Use 7-Zip or another AES ZIP compatible application. Python's built-in zipfile and some default archive tools cannot decrypt this format.

Alternatively, use Python:

```sh
python3 -m pip install pyzipper
python3 - <<'PY'
from pathlib import Path
from getpass import getpass
import os
import pyzipper
out = Path('delivery-local')
out.mkdir(mode=0o700, exist_ok=False)
with pyzipper.AESZipFile('delivery.zip') as archive:
    archive.setpassword(getpass('Passphrase: ').encode('utf-8'))
    for name in ('repo_key', 'START.md'):
        data = archive.read(name)
        fd = os.open(out / name, os.O_WRONLY | os.O_CREAT | os.O_EXCL, 0o600)
        with os.fdopen(fd, 'wb') as file:
            file.write(data)
print('Read delivery-local/START.md for complete instructions.')
PY
```

The passphrase, target details and usage instructions are not published in plaintext here. Do not publish the extracted files. Revoke the associated credential after use; deleting this repository cannot recall downloaded copies.
