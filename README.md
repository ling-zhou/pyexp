pyexp
=====
```
$ pyexp
python expect tool(powered by Ling Zhou) on the basis of pexpect
usage: pyexp <action> [options] [cmd] [args]
use 'pyexp {help | h} <action>' to print help on a specific action.

actions:
    help(h)
    scp
    rsync(rs)
    ssh

common options:
    -H hosts-file(line-fmt: host[:user[:pwd[:port]]], never with -h) *** login host(s)
    -h host[:user[:pwd[:port]]] (never with -H) ************************ login host
    -u default-user (optional, default: root) ************************** login user
    -p default-password (optional) ************************************* login pwd
    -P default-port (optional, default: 22) **************************** login port
    -s host-line(e.g. host[:user[:pwd[:port]]]) separator (optional, default: ':')
    -d print debug log
    --cmark comment(e.g. // my comment) mark (single line, optional, default: '//')
    --proxy proxy_ip:proxy_port (http proxy, optional)

notice:
    1. '-H' and '-h' can not be used at the same time.
    2. USER specified by -u can be overridden by USER in host[:USER[:pwd[:port]]]
    3. PASSWORD specified by -p can be overridden by PWD in host[:user[:PWD[:port]]]
    4. PORT specified by -P can be overridden by PORT in host[:user[:pwd[:PORT]]]
    5. a host-line-separator(default: ':') is needed if the member in between is not specified,
       for example: host::pwd, In this case, USER need be specified by -u.
    6. a special comment-mark(default: '//') is needed if it conflicts with USER or PASSWORD.

pyexp is a python expect tool, it can be used to:
    1. scp/rsync file/dir(s) from local to remote, or in reverse.
    2. ssh into host(s)(and execute command(s)).

report bug(s) to <zhou.0@foxmail.com>.

```
