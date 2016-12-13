
### Using `manpages`

This document is derived mostly from `man man` and its refernces.

It is possible to specify the exact /path/to/manpage in `man <manpage>`. 


#### Viewing all related man pages

Use `man <manpage> -wa` to see all manpages that would be opened

Another option: `man -aW man | xargs ls -l`

1. See what manpage files would be opened `man -w <manpage>` or `man --path <manpage>`
    - Supposedly `-W` gives one per line with no description
2. Use `man <manpage> -a` to sequentially view all manpages with the given title


#### man checks $PATH for manpages

If an application is on $PATH, man searches 

2. Specify folders: `man man -M /usr/share/man:/usr/local/share/man`
    - Can search and open local manpages this way
3. Or specify MANPATH in your man config.`


#### Configuration

Check out `$ man man.conf` for config file details

1. `man -C config_file`: Specify a configuration file
    - Default is `/private/etc/man.conf`

2. See also: `roff`, `groff`, `nroff`, `troff`, `ditroff`


#### Using a custom 'Pager'

This is probably best set in either $PAGER or $MANPAGER in `.bashrc`

1. default pager: `/usr/bin/less -is`
2. override: `man man -P "/usr/bin/less -Nis`
    - gives you line numbers
    - overrides `MANPAGER` environment variable
        - `MANPAGER` overrides `PAGER` environment variable
        - Consider setting this in `.bashrc`


#### Supporting and Coordinating Applications

1. `man -k <string>` - same as `apropos`
    - likely `man -k` is the most convenient method, "equivalent to apropos"
    - `apropos` - search the `whatis database` for "strings".
2. `man -f <complete keyword>` - same as `whatis`
    - `whatis` - search the `whatis database` for "complete keywords".
    - only displays complete word matches
    - the `whatis database` is created with the command `/usr/libexec/makewhatis`
3. `man -K <something>`
    - Search for a specified string in **all** man pages.
    - Continues search even after you say 'y' and open a manpage
    - still pretty slow, tested with `man -K vimtutor`



