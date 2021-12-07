# Setup
Guide to setting up various apps in Docker

## Matrix (weechat)
To connect to matrix, I am using weechat with the matrix plugin. It's currently running
off the Debian image because I wasn't able to find libolm-dev on alpine which I would have preferred.

**Rename the conf/matrix.conf.sample** to conf/matrix.conf

**(Optional) Update the homebase address**
The default configuration is set to connect to the matrix.org server. If you have
your own homeserver, change the `matrix_org.address` property to your custom address.

**Update your matrix credentials**
Update the username and password properties to match your correct credentials.
```
matrix_org.username = "--- replace me ---"
matrix_org.password = "--- replace me ---""
```

**(Optional) Custom weechat configurations**
If you want to use your own .weechat config files, change the `CONFIG_REPO` variable in the docker-compose.yml file.

**Run**
To run matrix execute the command:
```bash
$ docker-compose run matrix
```
