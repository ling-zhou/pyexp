pyexp
=====

python expect tool(powered by zhou ling) on the basis of pexpect
usage: pyexp <action> [options] [cmd] [args]
use 'pyexp {help | h} <action>' to print help on a specific action.

actions:
    help(h)
    scp
    rsync(rs)
    ssh

common options:
    -H hosts-file (line-fmt: host[:user[:pwd[:port]]], never with -h) ** login host(s)
    -h host[:user[:pwd[:port]]] (never with -H) ************************ login host
    -u default user (optional, default: user_00) *********************** login user
    -p default password (optional) ************************************* login pwd
    -P default port (optional, default: 36000) ************************* login port
    -s host-line(e.g. host[:user[:pwd[:port]]]) separator (optional, default: ':')
    -d print debug log
 
notice:
    1. '-H' and '-h' can not be used at the same time.
    2. USER specified by -u can be overridden by USER in host[:USER[:pwd[:port]]]
    3. PASSWORD specified by -p can be overridden by PWD in host[:user[:PWD[:port]]]
    4. PORT specified by -P can be overridden by PORT in host[:user[:pwd[:PORT]]]
    5. a separator(default: ':') is needed if the member in middle is not specified,
       for example: host::pwd, In this case, user need be specified by -u

pyexp is a python expect tool, it can be used to:
    1. scp/rsync file/dir(s) from local to remote, or in reverse.
    2. ssh into host(s)(and execute command(s)).

report bug(s) to <master@manpage.cn>.
