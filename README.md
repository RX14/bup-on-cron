bup-on-cron
===========
A script using `bup on` to create backups of remote machines.

Usage
-----
`bup-on-cron <ssh-args> <path-to-backupdirs.json>`

- `ssh-args` is passed to ssh when retrieving the `backupdirs.json` and also passed to `bup on`.
  This is usually set to `user@hostname`.
- `path-to-backupdirs.json` is the **REMOTE** path for `backupdirs.json`. This is retrieved using `cat` over SSH.


`backupdirs.json`
-----------------
`bup-on-cron` uses a file called `backupdirs.json` located on the remote machine to describe where to back up.
The file consists of a JSON hash of path to name, for example:
```json
{
  "/data/znc": "znc",
  "/data/nginx": "nxinx"
}
```
There is also a substitution mode where and array of names is substituted into a directory path
(using `$$` as the substituted value), for example:
```json
{
  "/data/$$/": [
    "znc",
    "nginx
  ]
}
```
The above example produces identical results to the previous example.
