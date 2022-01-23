pe(Python Expect)
======
```
$ pe
usage: pe <action> [options] [command] [args]

use 'pe help <action>' to print help for a specific action

actions:
    help (h)
    ssh
    scp
    rsync (rs)
    example (ex)

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
    -s, --select
        optional, select one host which will take effect, the others will be ignored.
    -j, --jobs N
        optional, runs up to N jobs in parallel in threads, defaults to 8.
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
       for example: host;;password
            in this case, default user will be used, and default user can be overridden by -u.
    6. user defined single-line-field-separator must be specified if password contains ';'.
       for example: '1.2.3.4_@_root_@_my;/passwd_@_22 // this is comment'
       # pe ... --field-sep '_@_' ...
    7. user defined single-line-comment-separator must be specified if password contains '//'.
       for example: '1.2.3.4;root;my//passwd;22 !@# this is comment'
       # pe ... --comment-sep '!@#' ...

pe is an automation tool based on ssh and Pexpect, it can be used to:
    1. scp|rsync local file|dir(s) to remote, or in reverse.
    2. ssh into host(s) (and execute command|file).

report bugs to <https://github.com/ling-zhou/pyexp>.
```

```
$ pe example
# log into host.
$ pe -h 'host;user;passwd;port' ssh

# log into host and execute a command.
$ pe -h 'host;user;passwd;port' ssh 'ps -ef | grep python'

# log into host and execute a command with debug info printed.
$ pe -h 'host;user;passwd;port' ssh 'ps -ef | grep python' -d

# log into host and execute a local file.
$ pe -h 'host;user;passwd;port' ssh -e script_file

# log into hosts one by one, use '<C-d>' to exit current machine and enter next one,
# use '<C-d><C-c>' to exit the entire process.
$ pe -H hosts.txt ssh

# log into the selected host.
$ pe -H hosts.txt ssh -s

# log into hosts and execute a command in parallel.
$ pe -H hosts.txt ssh 'ps -ef | grep python'

# log into the selected host and execute a command.
$ pe -H hosts.txt ssh 'ps -ef | grep python' -s

# log into hosts and execute a local file in parallel.
$ pe -H hosts.txt ssh -e script_file -j 5

# scp local file(s) and dir(s) to remote_dir on hosts in parallel.
$ pe -H hosts.txt scp local_file1 local_dir2 local_file3 remote_dir -j 8

# scp remote file(s) and dir(s) on hosts to local_dir in parallel.
$ pe -H hosts.txt scp -L remote_file1 remote_dir2 remote_file3 local_dir

# rsync local file(s) and dir(s) to remote_dir on hosts in parallel.
$ pe -H hosts.txt rsync local_file1 local_dir2 local_file3 remote_dir -j 8

# rsync remote file(s) and dir(s) on hosts to local_dir in parallel.
$ pe -H hosts.txt rsync -L remote_file1 remote_dir2 remote_file3 local_dir

# when separators do not meet the requirements, you can specify your own.
$ cat hosts.txt
www.abc.com@@user1@@pass1@@22 ^_^ this is host1
1.2.3.4@@user2@@pass2@@222 ^_^ this is host2
$ pe -H hosts.txt ssh 'ls -l' --field-sep '@@' --comment-sep '^_^'
```
