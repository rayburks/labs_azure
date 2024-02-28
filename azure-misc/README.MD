
# Problems to login with az cli

## Problems with computer time and time zone

```bash
> az login
To sign in, use a web browser to open the page https://microsoft.com/devicelogin and enter the code L3PPY67LU to authenticate.
The command failed with an unexpected error. Here is the traceback:
0. The ID token is not yet valid. Make sure your computer's time and time zone are both correct. Current epoch = 1709112801.  The id_token was: {
......
```

For WSL run the following command:

```bash
sudo hwclock -s
```

