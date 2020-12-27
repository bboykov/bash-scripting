# Useful Bash Resources

## Resources


- [Bash Guide][bash-guide]
- [Bash FAQ][bash-faq]
- [Bash Pitfalls][bash-pitfalls]
- [Bash-Hackers Wiki][bash-hacker-wiki]
- [Shellcheck][shellcheck] provides shell script guidelines and help.

[bash-guide]: http://mywiki.wooledge.org/BashGuide
[bash-faq]: http://mywiki.wooledge.org/BashFAQ
[bash-hacker-wiki]: https://wiki.bash-hackers.org/
[bash-pitfalls]: https://mywiki.wooledge.org/BashPitfalls
[shellcheck]: http://www.shellcheck.net/

## Techniques (tips and tricks)

### Handle command-line options (positional parameters)

The day will come when you want to give arguments to your scripts. These arguments are known as positional parameters.

- [BashFAQ/035][BashFAQ/035]
- [Bash Hakers Wiki: Handling positional parameters][bhw-posparams]

[BashFAQ/035]: http://mywiki.wooledge.org/BashFAQ/035
[bhw-posparams]: https://wiki.bash-hackers.org/scripting/posparams


### Global boolean "flags" implemented as functions

```bash
### cut ###
filename_only () { false; }
line_numbers  () { false; }
inverted      () { false; }

### cut ###

    # Process options
    while getopts :ilnxv opt; do
        case $opt in
            l) filename_only () { true; } ;;
            n) line_numbers  () { true; } ;;
            v) inverted      () { true; } ;;
            i) shopt -s nocasematch ;;
            x) pattern_fmt='^%s$' ;;
            ?) echo "Unknown option: $OPTARG" >&2 ;;
        esac
    done
    shift $((OPTIND - 1))

### cut ###
```

Source: [glennj's solution to the grep task](https://exercism.io/tracks/bash/exercises/grep/solutions/1b6e4d45871a4810829d0294ae7112da)
