pyexp
=====
```
$ pyexp
usage: pyexp <action> [options] [command] [args]

use 'pyexp help <action>' to print help for a specific action

actions:
    help (h)
    ssh
    scp
    rsync (rs)

common-options:
    -H, --Host hosts-file
        line-format: host;user;password;port, do not use it with '-h', no default value.
    -h, --host host;user;password;port
        do not use it with '-H', no default value.
    -u, --user default-user
        optional, defaults to 'root'.
    -p, --password default-password
        optional, defaults to 'x'.
    -P, --port default-port
        optional, defaults to '22'.
    -d, --debug
        optional, prints debug info.
    -j, --jobs N
        optional, runs up to N jobs concurrently in threads, defaults to 8.
    --field-sep single-line-field-separator
        optional, defaults to ';'.
    --comment-sep single-line-comment-separator
        optional, defaults to '//'.
    --proxy http_proxy_ip:http_proxy_port
        optional, no default value.

attentions:
    1. '-H' and '-h' can not be used together.
    2. user specified by '-u' can be overridden by USER in 'host;USER;password;port'.
    3. password specified by '-p' can be overridden by PASSWORD in 'host;user;PASSWORD;port'.
    4. port specified by '-P' can be overridden by PORT in 'host;user;password;PORT'.
    5. field-separator is needed if the member in between is not specified,
       for example: host::password
            in this case, default user will be used, and default user can be overridden by -u.
    6. user defined single-line-field-separator must be specified if password contains ';'.
       for example: '1.2.3.4_@_root_@_my:/passwd_@_22 // this is comment'
       # pyexp ... --field-sep '_@_' ...
    7. user defined single-line-comment-separator must be specified if PASSWORD contains '//'.
       for example: '1.2.3.4:root:my//passwd:22 !@# this is comment'
       # pyexp ... --comment-sep '!@#' ...

pyexp is an automation tool based on ssh and Pexpect, it can be used to:
    1. scp/rsync file/dir(s) from local to remote, or in reverse.
    2. ssh into host(s)(and execute command(s)).

report bug(s) to <https://github.com/ling-zhou/pyexp>.

```
