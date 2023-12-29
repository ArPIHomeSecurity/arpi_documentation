The secrets are stored in the database in a hashed format.
When you need to replace a hashed value you can use the following
method to generate it.

1. Login to the device
```bash
ssh -i arpi_rsa argus@arpi.local
```

2. Generate new registration code hash
```bash
cd server
# generate hashed value
./src/hash.py ABCD1234
a02910754569e36ad9209a1ca9b3358ff947ebb26c9c8f8006d617090cf56db3
```
