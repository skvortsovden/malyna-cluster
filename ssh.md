# SSH

## Troubleshooting

### WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!

When re-installing an operating system, the SSH host keys will be regenerated. This will cause the following error when trying to connect to the server:

```@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
```

To fix this, you need to remove the old host key from your `~/.ssh/known_hosts` file. You can do this by running the following command:

```
ssh-keygen -R <hostname>
```

or 

```
ssh-keygen -R <IP address>
```