
You can access the system via SSH. The SSH server is running on port 22. You can use the following command to connect to the system:

```bash
# with password authentication enabled
ssh argus@arpi.local

# with password authentication disabled
ssh -i ~/.ssh/id_rsa argus@arpi.local
```

The default password is `Argus.1234`.

* See the [Users SSH keys](../end_users/users.md/#ssh-keys) section.
* See the [Network terminal access](../end_users/network.md#terminal-access) section.
