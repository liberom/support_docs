### Compile and Install Bash

Source: https://www.gnu.org/software/bash/manual/html_node/Basic-Installation

Standard commands to compile the Bash source code and install it along with its associated files like manual pages and message translations. 'make install' may require elevated privileges, hence the 'sudo' option.

```bash
make
make install

```

```bash
sudo make install

```

--------------------------------

### Simulate Bash Installation with DESTDIR

Source: https://www.gnu.org/software/bash/manual/html_node/Installation-Names

This example demonstrates how to simulate the installation of Bash without actually modifying the system. The DESTDIR variable is used to specify a temporary root directory for the installation, allowing you to preview where files would be placed. This is useful for testing or verifying installation paths.

```bash
mkdir /fs1/bash-install
make install DESTDIR=/fs1/bash-install
```

--------------------------------

### Specify Separate Bash Installation Prefixes with make install

Source: https://www.gnu.org/software/bash/manual/html_node/Installation-Names

This example illustrates how to set separate installation prefixes for architecture-specific files (exec_prefix) and architecture-independent files (prefix) when installing Bash using 'make install'. This provides granular control over where different types of files are installed.

```bash
make install exec_prefix=/path/for/executables prefix=/path/for/data
```

--------------------------------

### Configure Bash Installation

Source: https://www.gnu.org/software/bash/manual/html_node/Basic-Installation

The 'configure' script prepares the Bash source code for compilation by detecting system-specific settings and creating Makefiles. It may require 'sh' prefix on older System V systems with csh. Running './configure --help' provides a list of available options.

```bash
cd /path/to/bash/source
./configure

```

```bash
sh ./configure

```

```bash
bash-4.2$ ./configure --help

```

--------------------------------

### Build Bash in Separate Directory

Source: https://www.gnu.org/software/bash/manual/html_node/Basic-Installation

This demonstrates how to compile Bash in a directory distinct from the source code location, which is useful for building for multiple architectures. It involves creating a new directory, changing into it, and then running the configure script with the full path to the source.

```bash
mkdir /usr/local/build/bash-4.4
cd /usr/local/build/bash-4.4
bash /usr/local/src/bash-4.4/configure
make

```

--------------------------------

### Install Bash Completion Function for `cd`

Source: https://www.gnu.org/software/bash/manual/html_node/A-Programmable-Completion-Example

This command installs the `_comp_cd` Bash completion function for the `cd` builtin. It uses `complete -F` to specify the function and several `-o` options to control Readline's behavior, such as treating completions as filenames, quoting them appropriately, and not appending spaces.

```bash
# Tell readline to quote appropriate and append slashes to directories;
# use the bash default completion for other arguments
complete -o filenames -o nospace -o bashdefault -F _comp_cd cd

```

--------------------------------

### Bash: Pattern Substitution Examples

Source: https://www.gnu.org/software/bash/manual/html_node/Shell-Parameter-Expansion

Demonstrates how pattern substitution works in Bash, including handling of '&' and quoted replacement strings.

```bash
var=abcdef
rep='& '
echo ${var/abc/& }
echo "${var/abc/& }"
echo ${var/abc/$rep}
echo "${var/abc/$rep}"
```

```bash
var=abcdef
rep='& '
echo ${var/abc/\& }
echo "${var/abc/\& }"
echo ${var/abc/"& "}
echo ${var/abc/"$rep"}
```

```bash
var=abcdef
rep='\&xyz'
echo ${var/abc/\&xyz}
echo ${var/abc/$rep}
```

--------------------------------

### Specify Bash Installation Prefix with make install

Source: https://www.gnu.org/software/bash/manual/html_node/Installation-Names

This example shows how to override the default installation prefix for Bash during the 'make install' process. By specifying the 'prefix' variable, you can direct 'make install' to place files in a different directory than the default /usr/local. This allows for custom installation locations.

```bash
make install prefix=/path/to/custom/prefix
```

--------------------------------

### Bash Job Manipulation Examples

Source: https://www.gnu.org/software/bash/manual/html_node/Job-Control-Basics

Shows examples of how to manipulate job states using shell commands. This includes bringing a job to the foreground or resuming it in the background.

```bash
# Bring job 1 to the foreground
%1

# Resume job 1 in the background
%1 &

```

--------------------------------

### Bash 'set -o option-name' Examples

Source: https://www.gnu.org/software/bash/manual/html_node/The-Set-Builtin

Provides examples of using '-o option-name' to set specific shell options, such as 'errexit' (equivalent to '-e'), 'noglob' (equivalent to '-f'), and 'pipefail'. It also shows how to display current option settings.

```bash
# Set 'errexit' option (same as -e)
set -o errexit

# Set 'noglob' option (same as -f)
set -o noglob

# Set 'pipefail' option
set -o pipefail

# Display current shell options settings
set -o

# Display 'set' commands to recreate current option settings
set +o
```

--------------------------------

### Bash Job Specification Examples

Source: https://www.gnu.org/software/bash/manual/html_node/Job-Control-Basics

Illustrates various ways to refer to jobs in Bash using job specifications. This includes referencing by job number, command name prefix, and substrings within the command line.

```bash
# Refer to job number 1
%1

# Refer to a job whose command starts with 'ce'
%ce

# Refer to any job containing 'ce' in its command line
%?ce

# Refer to the current job
%+
%%
%

# Refer to the previous job
%-

```

--------------------------------

### Install MO Files using TEXTDOMAINDIR and Environment Variables

Source: https://www.gnu.org/software/bash/manual/html_node/Creating-Internationalized-Scripts

Installs compiled MO files into the appropriate directory structure for gettext to find them. It sets the TEXTDOMAIN and TEXTDOMAINDIR environment variables to specify the message domain and the base directory for translations.

```bash
TEXTDOMAIN=example
TEXTDOMAINDIR=/usr/local/share/locale

cp es.mo ${TEXTDOMAINDIR}/es/LC_MESSAGES/${TEXTDOMAIN}.mo
cp eo.mo ${TEXTDOMAINDIR}/eo/LC_MESSAGES/${TEXTDOMAIN}.mo
```

--------------------------------

### Bash Job Notification Example

Source: https://www.gnu.org/software/bash/manual/html_node/Job-Control-Basics

Demonstrates the typical output format when Bash starts a job asynchronously. It shows the job number and the process ID of the last process in the pipeline.

```bash
[1] 25647

```

--------------------------------

### Clean Bash Build Files

Source: https://www.gnu.org/software/bash/manual/html_node/Basic-Installation

Commands to remove compiled object files and generated configuration files from the source directory. 'make clean' removes object files, while 'make distclean' also removes files created by 'configure', allowing for a fresh configuration.

```bash
make clean

```

```bash
make distclean

```

--------------------------------

### Bash Brace Expansion Example

Source: https://www.gnu.org/software/bash/manual/html_node/Brace-Expansion

Demonstrates basic brace expansion in Bash, where strings with a common prefix and suffix are generated. The expansion preserves the left-to-right order of elements within the braces.

```bash
bash$ echo a{d,c,b}e
ade ace abe
```

--------------------------------

### Using mkclone to Create a Build Tree for Multiple Architectures

Source: https://www.gnu.org/software/bash/manual/html_node/Compiling-For-Multiple-Architectures

This command uses the 'mkclone' script to create a build directory for compiling Bash. It sets up symbolic links back to the source directory, allowing for efficient multi-architecture builds. This method requires Bash to be installed for at least one architecture prior to execution.

```bash
bash /usr/gnu/src/bash-2.0/support/mkclone -s /usr/gnu/src/bash-2.0 .
```

--------------------------------

### Bash Completion Function for `cd`

Source: https://www.gnu.org/software/bash/manual/html_node/A-Programmable-Completion-Example

This Bash function, `_comp_cd`, provides programmable completions for the `cd` builtin. It handles tilde expansion, searches directories in `$CDPATH`, and supports the `cdable_vars` shell option. It modifies `IFS` to handle filenames with spaces and populates the `COMPREPLY` array with possible completions. It relies on `compgen -d` for directory completions and `compgen -v` for variable completions.

```bash
# A completion function for the cd builtin
# based on the cd completion function from the bash_completion package
_comp_cd()
{
    local IFS=$' \t\n'    # normalize IFS
    local cur _skipdot _cdpath
    local i j k

    # Tilde expansion, which also expands tilde to full pathname
    case "$2" in
    \~*)    eval cur="$2" ;; 
    *)      cur=$2 ;; 
    esac

    # no cdpath or absolute pathname -- straight directory completion
    if [[ -z "${CDPATH:-}" ]] || [[ "$cur" == @(./*|../*|/*) ]]; then
        # compgen prints paths one per line; could also use while loop
        IFS=$'\n'
        COMPREPLY=( $(compgen -d -- "$cur") )
        IFS=$' \t\n'
    # CDPATH+directories in the current directory if not in CDPATH
    else
        IFS=$'\n'
        _skipdot=false
        # preprocess CDPATH to convert null directory names to .
        _cdpath=${CDPATH/#:/.:}
        _cdpath=${_cdpath//::/:.:}
        _cdpath=${_cdpath/%:/:.}
        for i in ${_cdpath//:/$'
'};
        do
            if [[ $i -ef . ]]; then _skipdot=true; fi
            k="${#COMPREPLY[@]}"
            for j in $( compgen -d -- "$i/$cur" ); 
            do
                COMPREPLY[k++]=${j#$i/}        # cut off directory
            done
        done
        $_skipdot || COMPREPLY+=( $(compgen -d -- "$cur") )
        IFS=$' \t\n'
    fi

    # variable names if appropriate shell option set and no completions
    if shopt -q cdable_vars && [[ ${#COMPREPLY[@]} -eq 0 ]]; then
        COMPREPLY=( $(compgen -v -- "$cur") )
    fi

    return 0
}

```

--------------------------------

### Readline Active Region Start Color Example

Source: https://www.gnu.org/software/bash/manual/html_node/Readline-Init-File-Syntax

Illustrates setting the `active-region-start-color` variable, which controls the text color and background for the active region. The value should be a terminal escape sequence. This variable is reset when the terminal type changes.

```bash
set active-region-start-color "\e[01;33m"
```

--------------------------------

### Enable Readline Blink Matching Paren

Source: https://www.gnu.org/software/bash/manual/html_node/Readline-Init-File-Syntax

An example of setting the `blink-matching-paren` variable to 'on'. When enabled, Readline attempts to briefly move the cursor to an opening parenthesis when a closing parenthesis is inserted. The default is 'off'.

```bash
set blink-matching-paren on
```

--------------------------------

### Bash case Statement Syntax and Example

Source: https://www.gnu.org/software/bash/manual/html_node/Conditional-Constructs

The `case` command in Bash provides a way to match a word against multiple patterns and execute corresponding commands. It's useful for handling different scenarios based on input values. The example demonstrates matching an animal name to determine the number of legs.

```bash
case word in
    [ [(] pattern [| pattern]...) command-list ;;]...
esac

```

```bash
echo -n "Enter the name of an animal: "
read ANIMAL
echo -n "The $ANIMAL has "
case $ANIMAL in
  horse | dog | cat) echo -n "four";;
  man | kangaroo ) echo -n "two";;
  *) echo -n "an unknown number of";;
esac
echo " legs."

```

--------------------------------

### Readline Active Region End Color Example

Source: https://www.gnu.org/software/bash/manual/html_node/Readline-Init-File-Syntax

Shows how to set the `active-region-end-color` variable to restore the normal terminal display appearance after the active region. Similar to the start color, this value must be a terminal escape sequence and is reset on terminal type changes.

```bash
set active-region-end-color "\e[0m"
```

--------------------------------

### Tracking Shell Uptime with SECONDS

Source: https://www.gnu.org/software/bash/manual/html_node/Bash-Variables

Details the `SECONDS` variable, which expands to the number of seconds since the shell started. Assigning a value to `SECONDS` resets the counter.

```bash
# Get seconds since shell start
echo "Seconds elapsed: $SECONDS"

# Reset the counter
SECONDS=0
```

--------------------------------

### Include Init File Directive (Bash)

Source: https://www.gnu.org/software/bash/manual/html_node/Conditional-Init-Constructs

This directive allows you to include the contents of another Readline initialization file. In this example, it reads configurations from '/etc/inputrc'. This is useful for organizing settings into multiple files or for using system-wide configurations.

```bash
$include /etc/inputrc

```

--------------------------------

### Conditional Init Construct: Version Check (Bash)

Source: https://www.gnu.org/software/bash/manual/html_node/Conditional-Init-Constructs

This example demonstrates how to conditionally set Readline variables based on the version of Readline being used. It checks if the version is 7.0 or newer and enables 'show-mode-in-prompt' if true. This is useful for enabling features that were introduced in specific Readline versions.

```bash
$if version >= 7.0
set show-mode-in-prompt on
$endif

```

--------------------------------

### Set Readline Editing Mode to Vi

Source: https://www.gnu.org/software/bash/manual/html_node/Readline-Init-File-Syntax

An example of setting a Readline variable to change the editing mode. This specific example switches from the default Emacs-like key bindings to vi line editing commands. Variable names and values are generally case-insensitive.

```bash
set editing-mode vi
```

--------------------------------

### Bash: Backslash and Regex Pattern Matching

Source: https://www.gnu.org/software/bash/manual/html_node/Conditional-Constructs

Demonstrates how backslashes are interpreted differently by the shell and regular expressions, affecting pattern matching. It shows examples of quoted and unquoted patterns and their impact on matching literal characters.

```bash
pattern='\\.'

[[ . =~ $pattern ]]
[[ . =~ \\. ]]

[[ . =~ "$pattern" ]]
[[ . =~ '\\.' ]]

```

```bash
[[ . =~ "[.]" ]]
```

--------------------------------

### Bash Brace Expansion with Sequence Expression

Source: https://www.gnu.org/software/bash/manual/html_node/Brace-Expansion

Shows brace expansion using a sequence expression with letters. This generates a range of characters lexicographically between the specified start and end points.

```bash
chown root /usr/{ucb/{ex,edit},lib/{ex?.?*,how_ex}}
```

--------------------------------

### Bash Programmable Completion: Add Prefix to Completions (-P)

Source: https://www.gnu.org/software/bash/manual/html_node/Programmable-Completion-Builtins

Adds a specified prefix to the beginning of each possible completion after all other options have been processed. This is useful for ensuring completions start with a certain string.

```bash
# Example usage:
# compspec -P "/path/to/"
```

--------------------------------

### Conditional Init Construct: Variable Check (Bash)

Source: https://www.gnu.org/software/bash/manual/html_node/Conditional-Init-Constructs

This example illustrates how to conditionally set Readline variables based on the current editing mode. It checks if the editing mode is 'emacs' and, if so, enables 'show-mode-in-prompt'. This is equivalent to using 'mode=emacs' but demonstrates the variable comparison syntax.

```bash
$if editing-mode == emacs
set show-mode-in-prompt on
$endif

```

--------------------------------

### Bash select Construct for Menus

Source: https://www.gnu.org/software/bash/manual/html_node/Conditional-Constructs

The `select` construct in Bash is designed for creating interactive menus. It presents a list of items to the user, prompts for input, and executes commands based on the user's selection. The example shows selecting a filename from the current directory.

```bash
select name [in words ...]; do commands; done

```

```bash
select fname in *;
do
	echo you picked $fname \($REPLY\)
	break;
done

```

--------------------------------

### Bash: Manage Positional Parameters with -- and -

Source: https://www.gnu.org/software/bash/manual/html_node/The-Set-Builtin

The '--' argument signifies the end of options, treating all subsequent arguments as positional parameters, even if they start with '-'. The '-' argument also signals the end of options and assigns remaining arguments to positional parameters, while also turning off '-x' and '-v' options.

```bash
# Example using --
./my_script.sh -- arg1 arg2 "arg with spaces"

# Example using -
./my_script.sh - arg1 arg2

# Example with no arguments after --
./my_script.sh --

# Example with no arguments after -
./my_script.sh -
```

--------------------------------

### Get Number of Elements in Indexed Array in Bash

Source: https://www.gnu.org/software/bash/manual/html_node/Arrays

Expands to the total number of elements in an indexed array when the subscript is '@' or '*'. This provides a count of all items stored in the array.

```bash
echo "${#my_array[@]}"
```

--------------------------------

### Sample Readline Init File Configuration

Source: https://www.gnu.org/software/bash/manual/html_node/Sample-Init-File

This is a sample inputrc file for the GNU Readline library. It shows how to set variables, define key bindings for different editing modes (emacs), and include conditional configurations for specific programs like Bash and Ftp. It also demonstrates macro creation for complex commands.

```bash
# This file controls the behavior of line input editing for
# programs that use the GNU Readline library.  Existing
# programs include FTP, Bash, and GDB.
#
# You can re-read the inputrc file with C-x C-r.
# Lines beginning with '#' are comments.
#
# First, include any system-wide bindings and variable
# assignments from /etc/Inputrc
$include /etc/Inputrc

#
# Set various bindings for emacs mode. 

set editing-mode emacs 

$if mode=emacs

Meta-Control-h:	backward-kill-word	Text after the function name is ignored

#
# Arrow keys in keypad mode
#
#"\M-OD":        backward-char
#"\M-OC":        forward-char
#"\M-OA":        previous-history
#"\M-OB":        next-history
#
# Arrow keys in ANSI mode
#
"\M-[D":        backward-char
"\M-[C":        forward-char
"\M-[A":        previous-history
"\M-[B":        next-history
#
# Arrow keys in 8 bit keypad mode
#
#"\M-\C-OD":       backward-char
#"\M-\C-OC":       forward-char
#"\M-\C-OA":       previous-history
#"\M-\C-OB":       next-history
#
# Arrow keys in 8 bit ANSI mode
#
#"\M-\C-[D":       backward-char
#"\M-\C-[C":       forward-char
#"\M-\C-[A":       previous-history
#"\M-\C-[B":       next-history

C-q: quoted-insert

$endif

# An old-style binding.  This happens to be the default.
TAB: complete

# Macros that are convenient for shell interaction
$if Bash
# edit the path
"\C-xp": "PATH=${PATH}\e\C-e\C-a\ef\C-f"
# prepare to type a quoted word --
# insert open and close double quotes
# and move to just after the open quote
"\C-x\"": "\"\"\C-b"
# insert a backslash (testing backslash escapes
# in sequences and macros)
"\C-x\\": "\\"
# Quote the current or previous word
"\C-xq": "\eb\"\ef\""
# Add a binding to refresh the line, which is unbound
"\C-xr": redraw-current-line
# Edit variable on current line.
"\M-\C-v": "\C-a\C-k$\C-y\M-\C-e\C-a\C-y="
$endif

# use a visible bell if one is available
set bell-style visible

# don't strip characters to 7 bits when reading
set input-meta on

# allow iso-latin1 characters to be inserted rather
# than converted to prefix-meta sequences
set convert-meta off

# display characters with the eighth bit set directly
# rather than as meta-prefixed characters
set output-meta on

# if there are 150 or more possible completions for a word, 
# ask whether or not the user wants to see all of them
set completion-query-items 150

# For FTP
$if Ftp
"\C-xg": "get \M-?"
"\C-xt": "put \M-?"
"\M-.": yank-last-arg
$endif

```

--------------------------------

### Bash Builtin: Exec Command

Source: https://www.gnu.org/software/bash/manual/html_node/Bourne-Shell-Builtins

The 'exec' command replaces the current shell process with a specified command. It can also be used with options to start a new shell process with a modified environment or name. If no command is provided, 'exec' performs shell option processing.

```bash
exec [-cl] [-a name] [command [arguments]]
```

--------------------------------

### Get Length of Indexed Array Element in Bash

Source: https://www.gnu.org/software/bash/manual/html_node/Arrays

Expands to the length of the string value of a specific indexed array element. This is useful for determining the character count of an array member.

```bash
echo "${#my_array[0]}"
```

--------------------------------

### Bash Positional Parameters Substring Expansion

Source: https://www.gnu.org/software/bash/manual/html_node/Shell-Parameter-Expansion

Extracts a substring from positional parameters. Offset specifies the starting parameter, and length specifies how many parameters to include. Negative offsets count from the end. `$0` is prefixed if offset is 0.

```bash
$ set -- 1 2 3 4 5 6 7 8 9 0 a b c d e f g h
$ echo ${@:7}
7 8 9 0 a b c d e f g h
$ echo ${@:7:0}

$ echo ${@:7:2}
7 8
$ echo ${@:7:-2}
bash: -2: substring expression < 0
$ echo ${@: -7:2}
b c
$ echo ${@:0}
./bash 1 2 3 4 5 6 7 8 9 0 a b c d e f g h
$ echo ${@:0:2}
./bash 1
$ echo ${@: -7:0}


```

--------------------------------

### Compound Assignment for Indexed Array in Bash

Source: https://www.gnu.org/software/bash/manual/html_node/Arrays

Assigns multiple values to an indexed array in a single statement. If subscripts are omitted, elements are assigned to consecutive indices starting from the next available index (or 0 if the array is empty).

```bash
my_array=(value1 value2 value3)
```

--------------------------------

### Bash Indexed Array Substring Expansion

Source: https://www.gnu.org/software/bash/manual/html_node/Shell-Parameter-Expansion

Extracts a substring from elements of an indexed array. Offset specifies the starting element, and length specifies how many elements to include. Negative offsets count from the end. This behaves similarly to positional parameters.

```bash
$ array=(0 1 2 3 4 5 6 7 8 9 0 a b c d e f g h)
$ echo ${array[@]:7}
7 8 9 0 a b c d e f g h
$ echo ${array[@]:7:2}
7 8
$ echo ${array[@]: -7:2}
b c
$ echo ${array[@]: -7:-2}
bash: -2: substring expression < 0
$ echo ${array[@]:0}
0 1 2 3 4 5 6 7 8 9 0 a b c d e f g h
$ echo ${array[@]:0:2}
0 1
$ echo ${array[@]: -7:0}


```

--------------------------------

### Display Help Information for Bash Builtins

Source: https://www.gnu.org/software/bash/manual/html_node/Bash-Builtins

The 'help' command provides information about Bash builtin commands. When a pattern is specified, it offers detailed help for matching commands. Without a pattern, it lists all available builtins and compound commands. Options like '-d' can modify the output to show short descriptions.

```bash
help
help pattern
help -d pattern
```

--------------------------------

### Executing Commands Before Prompt with PROMPT_COMMAND

Source: https://www.gnu.org/software/bash/manual/html_node/Bash-Variables

Illustrates how to execute commands before the primary prompt is displayed. The PROMPT_COMMAND variable can be set to a string or an array of strings, where each string is interpreted as a command.

```bash
# Example with a single command
PROMPT_COMMAND='echo "Before prompt"'

# Example with an array of commands
PROMPT_COMMAND=("command1 arg1" "command2")
```

--------------------------------

### Configuring Shell Options with SHELLOPTS

Source: https://www.gnu.org/software/bash/manual/html_node/Bash-Variables

Explains how the `SHELLOPTS` variable, a colon-separated list of enabled shell options, affects shell behavior. Options listed in `SHELLOPTS` are enabled before startup files are read.

```bash
# Example: Enable errexit and nounset
export SHELLOPTS="errexit:nounset"
```

--------------------------------

### Bash Brace Expansion for Directory Creation

Source: https://www.gnu.org/software/bash/manual/html_node/Brace-Expansion

Illustrates using brace expansion to create multiple directories with a common path and varying subdirectories. This is a common shorthand for repetitive directory creation.

```bash
mkdir /usr/local/src/bash/{old,new,dist,bugs}
```

--------------------------------

### General Completion Commands

Source: https://www.gnu.org/software/bash/manual/html_node/Commands-For-Completion

Commands for performing and listing general text completions.

```APIDOC
## General Completion Commands

### Description
These commands handle attempting and listing possible completions for text before the cursor.

### Method
N/A (These are Readline commands, not HTTP endpoints)

### Endpoint
N/A

### Parameters
N/A

### Request Example
N/A

### Response
#### Success Response (N/A)
N/A

#### Response Example
N/A

## `complete` (TAB)

### Description
Attempts to perform completion on the text before point. The completion logic is application-specific, with Bash trying programmable completions, variables, usernames, hostnames, commands, and finally filenames.

### Method
N/A

### Endpoint
N/A

## `possible-completions` (M-?)

### Description
Lists the possible completions of the text before point. The number of columns used for display is determined by `completion-display-width`, the `COLUMNS` environment variable, or the screen width.

### Method
N/A

### Endpoint
N/A

## `insert-completions` (M-*)

### Description
Inserts all possible completions of the text before point, separated by a space.

### Method
N/A

### Endpoint
N/A

## `menu-complete`

### Description
Similar to `complete`, but replaces the word to be completed with a single match. Repeated execution cycles through possible completions. An argument `n` moves `n` positions forward in the list; a negative argument moves backward.

### Method
N/A

### Endpoint
N/A

## `menu-complete-backward`

### Description
Identical to `menu-complete`, but moves backward through the list of possible completions.

### Method
N/A

### Endpoint
N/A

## `export-completions`

### Description
Performs completion and writes the list of possible completions to Readline’s output stream in a specific format: number of matches, word being completed, start/end offsets, and then each match on a new line. Handles cases with no matches, a single match, or multiple matches including a common prefix.

### Method
N/A

### Endpoint
N/A

## `delete-char-or-list`

### Description
Deletes the character under the cursor if not at the end of the line. At the end of the line, it behaves identically to `possible-completions`.

### Method
N/A

### Endpoint
N/A
```

--------------------------------

### Bash 'set' Command Syntax and Options

Source: https://www.gnu.org/software/bash/manual/html_node/The-Set-Builtin

This snippet shows the general syntax for the 'set' builtin command in Bash, including options for setting or unsetting shell attributes and arguments for positional parameters. It also covers displaying current option settings.

```bash
set [-abefhkmnptuvxBCEHPT] [-o option-name] [--] [-] [argument ...]
set [+abefhkmnptuvxBCEHPT] [+o option-name] [--] [-] [argument ...]
set -o
set +o
```

--------------------------------

### Enable Readline Colored Completion Prefix

Source: https://www.gnu.org/software/bash/manual/html_node/Readline-Init-File-Syntax

Demonstrates setting `colored-completion-prefix` to 'on'. This causes Readline to display the common prefix of possible completions in a different color, using definitions from `LS_COLORS` or a custom suffix.

```bash
set colored-completion-prefix on
```

--------------------------------

### Bash Shopt Options Explained

Source: https://www.gnu.org/software/bash/manual/html_node/The-Shopt-Builtin

This section details the various options available for the 'shopt' builtin command. These options control how 'shopt' modifies or displays shell settings.

```bash
# -s: Enable each optname.
# -u: Disable each optname.
# -q: Suppresses normal output; the return status indicates whether the optname is set or unset.
# -o: Restricts the values of optname to be those defined for the -o option to the `set` builtin.
```

--------------------------------

### History and Brace Expansion

Source: https://www.gnu.org/software/bash/manual/html_node/Commands-For-Completion

Commands for history-based completion and brace expansion.

```APIDOC
## History and Brace Expansion

### Description
Commands related to completing text based on command history and expanding braced text.

### Method
N/A

### Endpoint
N/A

### Parameters
N/A

### Request Example
N/A

### Response
#### Success Response (N/A)
N/A

#### Response Example
N/A

## `dynamic-complete-history` (M-TAB)

### Description
Attempts completion on the text before point, comparing it against history list entries for possible matches.

### Method
N/A

### Endpoint
N/A

## `dabbrev-expand`

### Description
Attempts menu completion on the text before point, comparing it against lines from the history list for possible matches.

### Method
N/A

### Endpoint
N/A

## `complete-into-braces` (M-{)

### Description
Completes the text before point into braces. This command is useful for generating multiple related commands or file paths.

### Method
N/A

### Endpoint
N/A
```

--------------------------------

### Controlling Prompt Directory Truncation with PROMPT_DIRTRIM

Source: https://www.gnu.org/software/bash/manual/html_node/Bash-Variables

Shows how to control the number of trailing directory components displayed in the prompt using the `\w` and `\W` escapes. Setting PROMPT_DIRTRIM to a positive integer truncates the path and replaces removed components with an ellipsis.

```bash
# Retain only the last 2 directory components
PROMPT_DIRTRIM=2
```

--------------------------------

### Using SELECT Prompt with PS3

Source: https://www.gnu.org/software/bash/manual/html_node/Bash-Variables

Explains the use of the PS3 variable to customize the prompt for the `select` command. If PS3 is not set, the `select` command defaults to using '#? ' as its prompt.

```bash
# Set a custom prompt for the select command
PS3='Choose an option: '
```

--------------------------------

### Conditional Init Construct: Application Check (Bash)

Source: https://www.gnu.org/software/bash/manual/html_node/Conditional-Init-Constructs

This snippet shows how to apply specific key bindings for a particular application, in this case, Bash. It defines a key sequence to quote the current or previous word, which is only active when Readline is used by Bash. This allows for application-specific customizations.

```bash
$if Bash
# Quote the current or previous word
"\C-xq": "\eb\"\ef\""
$endif

```

--------------------------------

### Accessing Readline Buffer with READLINE_* Variables

Source: https://www.gnu.org/software/bash/manual/html_node/Bash-Variables

Explains the `READLINE_LINE`, `READLINE_POINT`, `READLINE_MARK`, and `READLINE_ARGUMENT` variables, which provide access to the Readline line buffer, cursor position, mark position, and numeric arguments for commands defined with `bind -x`.

```bash
# Example usage within a bind -x command (conceptual)
bind -x '"C-x\C-e": "echo \"Line: $READLINE_LINE, Point: $READLINE_POINT\""'
```

--------------------------------

### Enable Readline Case-Insensitive Completion with Hyphen/Underscore Equivalence

Source: https://www.gnu.org/software/bash/manual/html_node/Readline-Init-File-Syntax

Demonstrates setting `completion-map-case` to 'on' in conjunction with `completion-ignore-case`. This makes hyphens ('-') and underscores ('_') equivalent during case-insensitive filename matching and completion. The default is 'off'.

```bash
set completion-map-case on
```

--------------------------------

### Bash ulimit Resource Limits

Source: https://www.gnu.org/software/bash/manual/html_node/Bash-Builtins

The 'ulimit' command is used to control the resources available to the shell and its child processes. It can set or display resource limits such as maximum stack size, CPU time, virtual memory, and more. Limits can be specified as hard, soft, or unlimited. Values are typically in 1024-byte increments, with exceptions for time and specific units.

```bash
ulimit -s
ulimit -t
ulimit -u
ulimit -v
ulimit -x
ulimit -P
ulimit -R
ulimit -T
```

--------------------------------

### Set Readline Variable Syntax

Source: https://www.gnu.org/software/bash/manual/html_node/Readline-Init-File-Syntax

Demonstrates the basic syntax for setting Readline variables within the init file. This allows customization of Readline's runtime behavior. The `set` command is used followed by the variable name and its desired value.

```bash
set variable value
```

--------------------------------

### Specific Type Completion Commands

Source: https://www.gnu.org/software/bash/manual/html_node/Commands-For-Completion

Commands for performing and listing completions for specific types like filenames, usernames, hostnames, and commands.

```APIDOC
## Specific Type Completion Commands

### Description
These commands are specialized for completing text based on specific types such as filenames, usernames, hostnames, and commands.

### Method
N/A

### Endpoint
N/A

### Parameters
N/A

### Request Example
N/A

### Response
#### Success Response (N/A)
N/A

#### Response Example
N/A

## `complete-filename` (M-/)

### Description
Attempts filename completion on the text before point.

### Method
N/A

### Endpoint
N/A

## `possible-filename-completions` (C-x /)

### Description
Lists the possible filename completions of the text before point.

### Method
N/A

### Endpoint
N/A

## `complete-username` (M-~)

### Description
Attempts completion on the text before point, treating it as a username.

### Method
N/A

### Endpoint
N/A

## `possible-username-completions` (C-x ~)

### Description
Lists the possible username completions of the text before point.

### Method
N/A

### Endpoint
N/A

## `complete-variable` (M-$)

### Description
Attempts completion on the text before point, treating it as a shell variable.

### Method
N/A

### Endpoint
N/A

## `possible-variable-completions` (C-x $)

### Description
Lists the possible shell variable completions of the text before point.

### Method
N/A

### Endpoint
N/A

## `complete-hostname` (M-@)

### Description
Attempts completion on the text before point, treating it as a hostname.

### Method
N/A

### Endpoint
N/A

## `possible-hostname-completions` (C-x @)

### Description
Lists the possible hostname completions of the text before point.

### Method
N/A

### Endpoint
N/A

## `complete-command` (M-!)

### Description
Attempts completion on the text before point, treating it as a command name. It matches against aliases, reserved words, shell functions, shell builtins, and executable filenames in that order.

### Method
N/A

### Endpoint
N/A

## `possible-command-completions` (C-x !)

### Description
Lists the possible command name completions of the text before point.

### Method
N/A

### Endpoint
N/A
```

--------------------------------

### Set Readline Completion Display Width

Source: https://www.gnu.org/software/bash/manual/html_node/Readline-Init-File-Syntax

Demonstrates setting the `completion-display-width` variable to control the number of screen columns used for displaying possible completion matches. A value of 0 displays matches one per line. The default is -1.

```bash
set completion-display-width 80
```

```bash
set completion-display-width 0
```

--------------------------------

### Bash Coprocess Syntax

Source: https://www.gnu.org/software/bash/manual/html_node/Coprocesses

Demonstrates the basic syntax for creating a coprocess in Bash, including optional naming and redirections. The coprocess runs asynchronously, establishing a two-way pipe with the executing shell.

```bash
coproc [NAME] command [redirections]
```

```bash
coproc NAME { command; }
```

```bash
coproc NAME compound-command
```

```bash
coproc compound-command
```

```bash
coproc simple-command
```

--------------------------------

### Enable Readline Colored Stats for Completions

Source: https://www.gnu.org/software/bash/manual/html_node/Readline-Init-File-Syntax

Shows how to enable `colored-stats` by setting it to 'on'. This feature displays possible completions in different colors based on their file type, using definitions from the `LS_COLORS` environment variable. The default is 'off'.

```bash
set colored-stats on
```

--------------------------------

### Setting POSIX Mode with set -o posix

Source: https://www.gnu.org/software/bash/manual/html_node/Bash-Variables

Demonstrates how to enable POSIX mode in Bash. This mode alters shell behavior to adhere more closely to the POSIX standard. It can be invoked via the --posix option or by executing 'set -o posix'.

```bash
set -o posix
```

--------------------------------

### Copyright and License Notice for GFDL Documents

Source: https://www.gnu.org/software/bash/manual/html_node/GNU-Free-Documentation-License

This snippet provides the standard copyright and permission notice to include in a document licensed under the GNU Free Documentation License (GFDL), version 1.3 or later. It specifies terms for copying, distribution, and modification, and notes the absence of Invariant Sections, Front-Cover Texts, and Back-Cover Texts.

```text
Copyright (C)  year  your name.
 Permission is granted to copy, distribute and/or modify this document
 under the terms of the GNU Free Documentation License, Version 1.3
 or any later version published by the Free Software Foundation;
 with no Invariant Sections, no Front-Cover Texts, and no Back-Cover
 Texts.  A copy of the license is included in the section entitled ``GNU
 Free Documentation License''.

```

--------------------------------

### Bash Shopt Compatibility Options

Source: https://www.gnu.org/software/bash/manual/html_node/The-Shopt-Builtin

The 'compatXX' options (e.g., 'compat31', 'compat42') control specific aspects of Bash's compatibility mode, allowing users to tailor its behavior to match older versions.

```bash
# compat31
# compat32
# compat40
# compat41
# compat42
# compat43
# compat44
# These control aspects of the shell’s compatibility mode (see Shell Compatibility Mode).
```

--------------------------------

### Enable Readline Case-Insensitive Completion

Source: https://www.gnu.org/software/bash/manual/html_node/Readline-Init-File-Syntax

Shows how to set `completion-ignore-case` to 'on' to enable case-insensitive filename matching and completion. The default value is 'off'.

```bash
set completion-ignore-case on
```

--------------------------------

### Bash: Conditional ~/.bashrc Execution in ~/.bash_profile

Source: https://www.gnu.org/software/bash/manual/html_node/Bash-Startup-Files

This snippet demonstrates a common pattern in ~/.bash_profile to conditionally source ~/.bashrc if it exists. This ensures that settings from ~/.bashrc are applied to interactive login shells.

```bash
if [ -f ~/.bashrc ]; then . ~/.bashrc; fi
```

--------------------------------

### Create Language-Specific PO Files using cp

Source: https://www.gnu.org/software/bash/manual/html_node/Creating-Internationalized-Scripts

Copies the template (.pot) file to a new file for a specific language (e.g., Spanish 'es.po'). This PO file will be manually edited to contain the translations for that language.

```bash
cp example.pot es.po
```

--------------------------------

### Debugging Command Echo with PS4

Source: https://www.gnu.org/software/bash/manual/html_node/Bash-Variables

Demonstrates how PS4 is used to indicate the prompt printed before a command line is echoed when the `-x` option is enabled. The first character of PS4 is replicated to show nesting levels.

```bash
# Set PS4 to display with indentation
PS4='+ \t '
```

--------------------------------

### Reading Input with REPLY Variable

Source: https://www.gnu.org/software/bash/manual/html_node/Bash-Variables

Shows how the `REPLY` variable is used by the `read` builtin command. When `read` is called without a variable name argument, the input line is stored in `REPLY`.

```bash
# Read input and store in REPLY
read
echo "You entered: $REPLY"
```

--------------------------------

### Directory Stack Builtins API

Source: https://www.gnu.org/software/bash/manual/html_node/Directory-Stack-Builtins

Documentation for the 'dirs', 'popd', and 'pushd' built-in commands for managing the Bash directory stack.

```APIDOC
## Directory Stack Builtins API

This section details the Bash built-in commands for manipulating the directory stack.

### `dirs` Command

#### Description
Displays the list of currently remembered directories in the directory stack. Options can modify the output format or clear the stack.

#### Method
Built-in Shell Command

#### Endpoint
`dirs [-clpv] [+N | -N]`

#### Parameters

##### Options
- **-c** (flag) - Clears the directory stack.
- **-l** (flag) - Produces a listing using full pathnames.
- **-p** (flag) - Prints the directory stack with one entry per line.
- **-v** (flag) - Prints the directory stack with one entry per line, prefixing each entry with its index.

##### Positional Arguments
- **+N** (integer) - Displays the Nth directory (counting from the left, starting with zero).
- **-N** (integer) - Displays the Nth directory (counting from the right, starting with zero).

#### Request Example
```bash
dirs -pv
```

#### Response
##### Success Response (0)
- **Output** (string) - The formatted list of directories in the stack.

##### Response Example
```
0	/home/user/project1
1	/home/user/documents
2	/home/user
```

### `popd` Command

#### Description
Removes elements from the directory stack. By default, it removes the top directory and changes to the new top directory.

#### Method
Built-in Shell Command

#### Endpoint
`popd [-n] [+N | -N]`

#### Parameters

##### Options
- **-n** (flag) - Suppress the normal change of directory when removing elements.

##### Positional Arguments
- **+N** (integer) - Remove the Nth directory (counting from the left, starting with zero).
- **-N** (integer) - Remove the Nth directory (counting from the right, starting with zero).

#### Request Example
```bash
popd +1
```

#### Response
##### Success Response (0)
- **Output** (string) - The final contents of the directory stack are displayed by `dirs`.
- **Return Status** (integer) - 0 on success.

##### Error Response
- **Return Status** (integer) - Non-zero if an invalid option is specified, the directory stack is empty, or N specifies a non-existent directory stack entry.

### `pushd` Command

#### Description
Adds a directory to the top of the directory stack, or rotates the stack. With no arguments, it exchanges the top two elements.

#### Method
Built-in Shell Command

#### Endpoint
`pushd [-n] [+N | -N | dir]`

#### Parameters

##### Options
- **-n** (flag) - Suppress the normal change of directory when rotating or adding directories.

##### Positional Arguments
- **+N** (integer) - Rotate the stack so the Nth directory (counting from the left, starting with zero) is at the top.
- **-N** (integer) - Rotate the stack so the Nth directory (counting from the right, starting with zero) is at the top.
- **dir** (string) - Make the specified directory the top of the stack.

#### Request Example
```bash
pushd /var/log
```

#### Response
##### Success Response (0)
- **Output** (string) - The final contents of the directory stack are displayed by `dirs`.
- **Return Status** (integer) - 0 on success.

##### Error Response
- **Return Status** (integer) - Non-zero if the `cd` builtin fails, the directory stack is empty, or N specifies a non-existent directory stack element.
```

--------------------------------

### Bash: Redirecting Input

Source: https://www.gnu.org/software/bash/manual/html_node/Redirections

Shows the general format for redirecting the standard input (file descriptor 0) of a command from a specified file. The file is opened for reading.

```bash
[n]<word

```

--------------------------------

### Bash: Redirecting Standard Output and Standard Error

Source: https://www.gnu.org/software/bash/manual/html_node/Redirections

Demonstrates how to redirect both standard output (file descriptor 1) and standard error (file descriptor 2) to a single file. The order of redirection is crucial for correct behavior.

```bash
ls > dirlist 2>&1

```

```bash
ls 2>&1 > dirlist

```

--------------------------------

### compgen Builtin

Source: https://www.gnu.org/software/bash/manual/html_node/Programmable-Completion-Builtins

Generates possible completion matches for a given word based on specified options.

```APIDOC
## compgen Builtin

### Description
Generate possible completion matches for `word` according to the options, which may be any option accepted by the `complete` builtin with the exceptions of -p, -r, -D, -E, and -I, and write the matches to the standard output.
If the -V option is supplied, `compgen` stores the generated completions into the indexed array variable `varname` instead of writing them to the standard output.

### Method
Builtin

### Endpoint
N/A (Shell builtin)

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
```bash
compgen -c bash
```

### Response
#### Success Response (0)
- **matches** (array of strings) - Possible completion matches written to standard output or stored in a variable.

#### Response Example
```
complete
compgen
continue
```
```

--------------------------------

### Dynamic Completion Loading Function in Bash

Source: https://www.gnu.org/software/bash/manual/html_node/Programmable-Completion

This Bash function demonstrates how to dynamically load completion specifications from files. It attempts to source a file named after the command being completed and returns an exit status of 124 if successful, signaling Bash to re-evaluate completions. This is useful for managing large sets of completions.

```bash
_completion_loader() {
    . "/etc/bash_completion.d/$1.sh" >/dev/null 2>&1 && return 124
}
complete -D -F _completion_loader -o bashdefault -o default

```

--------------------------------

### Configure Readline Bell Style

Source: https://www.gnu.org/software/bash/manual/html_node/Readline-Init-File-Syntax

Demonstrates setting the `bell-style` variable to control Readline's bell behavior. Options include 'none' to disable the bell, 'visible' for a visible bell, and 'audible' (the default) to attempt ringing the terminal's bell.

```bash
set bell-style none
```

```bash
set bell-style visible
```

```bash
set bell-style audible
```

--------------------------------

### Bash Shopt Option: direxpand

Source: https://www.gnu.org/software/bash/manual/html_node/The-Shopt-Builtin

This option controls the expansion of directory names. Further details on its specific behavior are not provided in the excerpt.

```bash
# direxpand
```

--------------------------------

### Bash: Redirecting Output

Source: https://www.gnu.org/software/bash/manual/html_node/Redirections

Illustrates the general format for redirecting the standard output (file descriptor 1) of a command to a specified file. The file is created if it doesn't exist or truncated if it does. The `noclobber` option can prevent overwriting existing files.

```bash
[n]>[|]word

```

--------------------------------

### Bash Shopt Builtin Usage

Source: https://www.gnu.org/software/bash/manual/html_node/The-Shopt-Builtin

This snippet shows the general syntax for the 'shopt' builtin command in Bash. It is used to enable, disable, or query optional shell behaviors.

```bash
shopt [-pqsu] [-o] [optname ...]
```

--------------------------------

### Compile PO Files to MO Message Catalogs using msgfmt

Source: https://www.gnu.org/software/bash/manual/html_node/Creating-Internationalized-Scripts

Compiles a human-readable PO translation file into an efficient binary MO (message catalog) file. The '-o' flag specifies the output file name.

```bash
msgfmt -o es.mo es.po
```

--------------------------------

### Bash 'set' Options: Export and Background Job Notification

Source: https://www.gnu.org/software/bash/manual/html_node/The-Set-Builtin

Demonstrates the '-a' option to mark variables for export and the '-b' option to immediately report the status of terminated background jobs. The '-b' option requires job control to be enabled.

```bash
# Set '-a' to export all variables created or modified
set -a

# Set '-b' to report background job status immediately (requires job control)
set -b
```

--------------------------------

### Set Readline Comment Begin String

Source: https://www.gnu.org/software/bash/manual/html_node/Readline-Init-File-Syntax

Illustrates setting the `comment-begin` variable, which defines the string inserted by the `insert-comment` command. The default value is '#'.

```bash
set comment-begin "#"
```

--------------------------------

### Bash: Trace Command Execution with set -x

Source: https://www.gnu.org/software/bash/manual/html_node/The-Set-Builtin

The `set -x` option, also known as `xtrace`, enables command tracing in Bash. It prints expanded commands and their arguments to standard error before execution, prefixed by the `PS4` variable. This is invaluable for debugging scripts.

```bash
# Enable command tracing
set -x

echo "This is a test message."
ls -l

# Disable command tracing
set +x
```

--------------------------------

### Bash: Non-interactive Script Execution with BASH_ENV

Source: https://www.gnu.org/software/bash/manual/html_node/Bash-Startup-Files

When Bash is invoked non-interactively to run a script, it checks the BASH_ENV environment variable. If set, Bash reads and executes commands from the file specified by its expanded value.

```bash
if [ -n "$BASH_ENV" ]; then . "$BASH_ENV"; fi
```

--------------------------------

### Generating Random Numbers with RANDOM

Source: https://www.gnu.org/software/bash/manual/html_node/Bash-Variables

Illustrates how the `RANDOM` variable generates a random integer between 0 and 32767 each time it is referenced. Assigning a value to `RANDOM` seeds the random number generator.

```bash
# Get a random number
random_num=$RANDOM

# Seed the random number generator
RANDOM=12345
```

--------------------------------

### Bash Programmable Completion Options

Source: https://www.gnu.org/software/bash/manual/html_node/Programmable-Completion-Builtins

This section outlines the different types of completions that can be specified for programmable completion in Bash, along with options for customizing the completion behavior.

```APIDOC
## Bash Programmable Completion Options

### Description
This section details various completion specifications that can be used with Bash's programmable completion feature. These specifications define how Bash should generate possible completions for commands, filenames, variables, and other shell elements.

### Completion Types:

*   **`alias`**: Names of aliases. May also be specified as `-a`.
*   **`command`**: Names of commands. May also be specified as `-c`.
*   **`directory`**: Directory names. May also be specified as `-d`.
*   **`export`**: Names of exported shell variables. May also be specified as `-e`.
*   **`file`**: File and directory names, similar to Readline’s filename completion. May also be specified as `-f`.
*   **`function`**: Names of shell functions.
*   **`group`**: Group names. May also be specified as `-g`.
*   **`helptopic`**: Help topics as accepted by the `help` builtin.
*   **`hostname`**: Hostnames, as taken from the file specified by the `HOSTFILE` shell variable.
*   **`job`**: Job names, if job control is active. May also be specified as `-j`.
*   **`keyword`**: Shell reserved words. May also be specified as `-k`.
*   **`running`**: Names of running jobs, if job control is active.
*   **`service`**: Service names. May also be specified as `-s`.
*   **`setopt`**: Valid arguments for the `-o` option to the `set` builtin.
*   **`shopt`**: Shell option names as accepted by the `shopt` builtin.
*   **`signal`**: Signal names.
*   **`stopped`**: Names of stopped jobs, if job control is active.
*   **`user`**: User names. May also be specified as `-u`.
*   **`variable`**: Names of all shell variables. May also be specified as `-v`.

### Customization Options:

*   **`-C command`**: Executes `command` in a subshell and uses its output for completions. Arguments are passed as with `-F`.
*   **`-F function`**: Executes the shell function `function` in the current shell environment. The function receives arguments describing the context of the completion. Completions are retrieved from the `COMPREPLY` array variable.
*   **`-G globpat`**: Expands the filename expansion pattern `globpat` to generate possible completions.
*   **`-P prefix`**: Adds `prefix` to the beginning of each possible completion.
*   **`-S suffix`**: Appends `suffix` to each possible completion.
*   **`-W wordlist`**: Splits `wordlist` by `IFS` characters and expands each word. Completions are members of the resulting list that match a prefix of the word being completed.
*   **`-X filterpat`**: Filters the list of possible completions using `filterpat`. A leading `!` negates the pattern.

### Return Value:

The return value is true unless an invalid option is supplied, an option is supplied without a required argument, an attempt is made to remove a completion specification for a non-existent name, or an error occurs during specification addition.
```

--------------------------------

### Enable Readline Binding of TTY Special Characters

Source: https://www.gnu.org/software/bash/manual/html_node/Readline-Init-File-Syntax

Shows how to set the `bind-tty-special-chars` variable to 'on' to enable Readline to bind control characters treated specially by the kernel's terminal driver to their Readline equivalents. The default is 'on'.

```bash
set bind-tty-special-chars on
```

--------------------------------

### Generate Completion Matches with compgen

Source: https://www.gnu.org/software/bash/manual/html_node/Programmable-Completion-Builtins

The 'compgen' builtin generates possible completion matches for a given word based on specified options. It can either write matches to standard output or store them in an indexed array variable. This is useful for custom completion scripts.

```bash
compgen [-V varname] [option] [word]
```

--------------------------------

### getopts

Source: https://www.gnu.org/software/bash/manual/html_node/Bourne-Shell-Builtins

Parses positional parameters, extracting options and their arguments for shell scripts and functions. It manages option parsing state using OPTIND and OPTARG.

```APIDOC
## getopts optstring name [arg ...]

### Description
`getopts` is used by shell scripts or functions to parse positional parameters and obtain options and their arguments. `optstring` contains the option characters to be recognized; if a character is followed by a colon, the option is expected to have an argument. Each time it is invoked, `getopts` places the next option in the shell variable `name`, and the index of the next argument to be processed into the variable `OPTIND`. `OPTIND` is initialized to 1 for each new shell invocation. When an option requires an argument, `getopts` places that argument into the variable `OPTARG`. `getopts` can report errors silently or print diagnostic messages. It returns true if an option is found, and false when it encounters the end of options or an error occurs.

### Method
Built-in

### Endpoint
N/A (Shell Built-in)

### Parameters
#### Path Parameters
N/A

#### Query Parameters
N/A

#### Request Body
N/A

### Request Example
```bash
while getopts "ab:c" opt; do
  case $opt in
    a) echo "Option a"
    ;; 
    b) echo "Option b with argument $OPTARG"
    ;; 
    c) echo "Option c"
    ;; 
    ?) echo "Invalid option: -$OPTARG"
    ;; 
  esac
done
```

### Response
#### Success Response (0 or 1)
- **status** (integer) - 0 if an option is found, 1 if end of options or error.
- **name** (string) - The next option character or '?' or ':' on error.
- **OPTARG** (string) - The argument to an option, if required.

#### Response Example
```json
{
  "status": 0,
  "name": "b",
  "OPTARG": "argument_for_b"
}
```
```

--------------------------------

### Bash Programmable Completion: Execute Command for Completions (-C)

Source: https://www.gnu.org/software/bash/manual/html_node/Programmable-Completion-Builtins

Specifies that a command should be executed in a subshell, and its output will be used as possible completions. Arguments are passed similarly to the -F option. This is useful for dynamic completion based on external command output.

```bash
# Example usage:
# compspec -C "ls -l"
```

--------------------------------

### Bash Shopt Option: checkhash

Source: https://www.gnu.org/software/bash/manual/html_node/The-Shopt-Builtin

When 'checkhash' is set, Bash verifies that a command found in the hash table actually exists before attempting execution. If not, it performs a standard path search.

```bash
# If this is set, Bash checks that a command found in the hash table exists before trying to execute it. If a hashed command no longer exists, Bash performs a normal path search.
```

--------------------------------

### complete Builtin

Source: https://www.gnu.org/software/bash/manual/html_node/Programmable-Completion-Builtins

Specifies how arguments to a command should be completed, or prints/removes existing completion specifications.

```APIDOC
## complete Builtin

### Description
Specify how arguments to each `name` should be completed. If the -p option is supplied, or if no options or names are supplied, print existing completion specifications in a way that allows them to be reused as input. The -r option removes a completion specification for each `name`, or, if no names are supplied, all completion specifications.

### Method
Builtin

### Endpoint
N/A (Shell builtin)

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
```bash
complete -c "ls"
complete -W "start stop" my_command
```

### Response
#### Success Response (0)
- **Output** (string) - If -p is used, prints existing completion specifications. Otherwise, modifies completion behavior.

#### Response Example
```bash
# Example output for 'complete -p'
complete -c ls
complete -W start stop my_command
```
```

--------------------------------

### Execute Command Before Each Simple Command with trap DEBUG

Source: https://www.gnu.org/software/bash/manual/html_node/Bourne-Shell-Builtins

The `trap DEBUG` command executes a specified action before every simple command, for loop, case command, select command, arithmetic command, conditional command, arithmetic for command, and before the first command in a shell function. This is useful for debugging and tracing command execution.

```bash
trap 'action' DEBUG
```

--------------------------------

### Bash Process Substitution Syntax

Source: https://www.gnu.org/software/bash/manual/html_node/Process-Substitution

Demonstrates the syntax for process substitution in Bash. The `<(list)` form reads output from a process, while `>(list)` writes input to a process. No spaces are allowed between the redirection operator and the parenthesis.

```bash
<(list)

```

```bash
>(list)

```

--------------------------------

### Bash Parameter Expansion: Default Value Substitution

Source: https://www.gnu.org/software/bash/manual/html_node/Shell-Parameter-Expansion

Demonstrates `${parameter:-word}` and `${parameter:=word}` for substituting default values when a parameter is unset or null. The first form only substitutes, while the second also assigns the default value to the parameter.

```bash
$ v=123
$ echo ${v-unset}
123
$ echo ${v:-unset-or-null}
123
$ unset v
$ echo ${v-unset}
unset
$ v=
$ echo ${v-unset}

$ echo ${v:-unset-or-null}
unset-or-null

```

```bash
$ unset var
$ : ${var=DEFAULT}
$ echo $var
DEFAULT
$ var=
$ : ${var=DEFAULT}
$ echo $var

$ var=
$ : ${var:=DEFAULT}
$ echo $var
DEFAULT
$ unset var
$ : ${var:=DEFAULT}
$ echo $var
DEFAULT

```

--------------------------------

### Bash 'set -k' for Environment Assignment

Source: https://www.gnu.org/software/bash/manual/html_node/The-Set-Builtin

Demonstrates the '-k' option, which causes all arguments in the form of assignment statements to be placed in the environment for a command. This differs from the default behavior where only assignments preceding the command name are exported.

```bash
# Place all assignment arguments in the environment
set -k
```

--------------------------------

### compopt Builtin

Source: https://www.gnu.org/software/bash/manual/html_node/Programmable-Completion-Builtins

The `compopt` builtin command is used to modify completion options for specified names or for the default, empty, or initial word completions.

```APIDOC
## compopt Builtin

### Description
Modifies completion options for specified names or for the currently-executing completion if no names are supplied. If no options are given, it displays the completion options for each name or the current completion.

### Method
```bash
compopt [-o option] [-DEI] [+o option] [name]
```

### Parameters

*   **`-o option`**: Specifies an option to be set.
*   **`+o option`**: Specifies an option to be unset.
*   **`-D`**: Applies other supplied options to the "default" command completion.
*   **`-E`**: Applies other supplied options to "empty" command completion.
*   **`-I`**: Applies other supplied options to completion on the initial word on the line.
*   **`name`**: The name for which to modify completion options. If omitted, applies to the current completion context.

### Options for `option`:

Valid values for `option` are those valid for the `complete` builtin (e.g., `bash`, `dir`, `file`, `group`, `helptopic`, `hostname`, `job`, `keyword`, `running`, `service`, `setopt`, `shopt`, `signal`, `stopped`, `user`, `variable`).

### Precedence of `-D`, `-E`, `-I`:

If multiple of these options are supplied, `-D` takes precedence over `-E`, and both take precedence over `-I`.

### Return Value:

The return value is true unless an invalid option is supplied, an attempt is made to modify options for a name with no existing completion specification, or an output error occurs.
```

--------------------------------

### Here Documents in Bash

Source: https://www.gnu.org/software/bash/manual/html_node/Redirections

Instructs the shell to read input from the current source until a line containing only the specified delimiter is encountered. This input becomes the standard input for a command. Leading tabs can be stripped if `<<-` is used.

```bash
[n]<<[−]word
        here-document
delimiter
```

--------------------------------

### Bash read Command with Line Editing and Completion

Source: https://www.gnu.org/software/bash/manual/html_node/Bash-Builtins

When input is from a terminal, `read` can use Readline for editing. The `-e` option uses Readline's default filename completion, while `-E` uses Bash's default completion, including programmable completion. The `-i` option pre-populates the editing buffer.

```bash
read -e -p "Enter command: " command
```

```bash
read -E -i "default_value" input
```

--------------------------------

### Specify Argument Completion Behavior with complete

Source: https://www.gnu.org/software/bash/manual/html_node/Programmable-Completion-Builtins

The 'complete' builtin defines how arguments for specific commands should be completed. It allows setting various completion actions, filters, and options to customize the completion process. Existing specifications can be printed or removed using the -p and -r options respectively.

```bash
complete [-abcdefgjksuv] [-o comp-option] [-DEI] [-A action]
[-G globpat] [-W wordlist] [-F function] [-C command]
[-X filterpat] [-P prefix] [-S suffix] name [name ...]
complete -pr [-DEI] [name ...]
```

--------------------------------

### Bash Arithmetic Expansion Syntax

Source: https://www.gnu.org/software/bash/manual/html_node/Arithmetic-Expansion

This snippet demonstrates the basic syntax for arithmetic expansion in Bash. It evaluates an arithmetic expression and replaces it with its resulting value. The expression undergoes parameter expansion, command substitution, and quote removal before evaluation. Empty strings resulting from expansions are treated as 0.

```bash
echo $(( 1 + 2 ))
# Output: 3

count=5
echo $(( count * 2 ))
# Output: 10

result=$(( (1 + 2) * 3 ))
echo $result
# Output: 9
```

--------------------------------

### Bash Invocation Syntax

Source: https://www.gnu.org/software/bash/manual/html_node/Invoking-Bash

Defines the general syntax for invoking the Bash shell with various options. It shows how to use single-character and long options, execute commands from a string, or read from standard input.

```bash
bash [long-opt] [-ir] [-abefhkmnptuvxdBCDHP] [-o option]
    [-O shopt_option] [argument ...]
bash [long-opt] [-abefhkmnptuvxdBCDHP] [-o option]
    [-O shopt_option] -c string [argument ...]
bash [long-opt] -s [-abefhkmnptuvxdBCDHP] [-o option]
    [-O shopt_option] [argument ...]
```

--------------------------------

### Bash let: Perform Arithmetic Operations

Source: https://www.gnu.org/software/bash/manual/html_node/Bash-Builtins

The `let` builtin command allows arithmetic to be performed on shell variables. It evaluates expressions according to shell arithmetic rules. The return status indicates the result of the last expression (0 for non-zero, 1 for zero).

```bash
let expression [expression ...]

```

--------------------------------

### Bash 'set -m' for Job Control and Monitoring

Source: https://www.gnu.org/software/bash/manual/html_node/The-Set-Builtin

Details the '-m' option, which enables job control. When enabled, processes run in separate process groups, and the shell reports the completion status of background jobs.

```bash
# Enable job control and monitor background jobs
set -m
```

--------------------------------

### Bash Shopt Option: checkwinsize

Source: https://www.gnu.org/software/bash/manual/html_node/The-Shopt-Builtin

The 'checkwinsize' option, enabled by default, makes Bash check the terminal window size after each external command and update 'LINES' and 'COLUMNS' if necessary.

```bash
# If set, Bash checks the window size after each external (non-builtin) command and, if necessary, updates the values of `LINES` and `COLUMNS`, using the file descriptor associated with stderr if it is a terminal. This option is enabled by default.
```

--------------------------------

### Bash: Enable Brace Expansion with set -B

Source: https://www.gnu.org/software/bash/manual/html_node/The-Set-Builtin

The `set -B` option enables brace expansion in Bash, allowing for the generation of strings from patterns enclosed in curly braces. This option is enabled by default in most Bash environments.

```bash
# Brace expansion is typically on by default, but can be explicitly enabled
set -B

echo file{1..3}.txt
# Output: file1.txt file2.txt file3.txt

echo {a,b,c}.log
# Output: a.log b.log c.log
```

--------------------------------

### Extract Translatable Strings using bash --dump-po-strings

Source: https://www.gnu.org/software/bash/manual/html_node/Creating-Internationalized-Scripts

This command extracts strings marked for translation (using $"...") from a Bash script into a gettext template file (.pot). The domain is a unique identifier for your script's translations.

```bash
bash --dump-po-strings scriptname > domain.pot
```

--------------------------------

### Bash Shopt Option: bash_source_fullpath

Source: https://www.gnu.org/software/bash/manual/html_node/The-Shopt-Builtin

When 'bash_source_fullpath' is enabled, filenames added to the 'BASH_SOURCE' array variable are converted to their full pathnames.

```bash
# If set, filenames added to the `BASH_SOURCE` array variable are converted to full pathnames (see Bash Variables).
```

--------------------------------

### Parse options in shell scripts

Source: https://www.gnu.org/software/bash/manual/html_node/Bourne-Shell-Builtins

The `getopts` command is used within shell scripts and functions to parse positional parameters, extracting options and their arguments. It manages option parsing state using `OPTIND` and `OPTARG`, and supports silent or verbose error reporting based on `optstring` and `OPTERR`.

```bash
getopts optstring name [arg ...]
```

--------------------------------

### hash

Source: https://www.gnu.org/software/bash/manual/html_node/Bourne-Shell-Builtins

Maintains a cache of looked-up directory prefixes for commands. It can be used to display or clear the command cache.

```APIDOC
## hash [-r] [-p filename] [-dt] [name]

### Description
The `hash` builtin is used to maintain a cache of looked-up directory prefixes for commands. The `-r` option clears the cache. The `-p filename` option forces `hash` to enter `filename` into the alias table. The `-d` option removes the alias for `name`. The `-t` option causes `hash` to print the alias for `name`. If `name` is supplied, only that name is added to or removed from the alias table. If no options are supplied, `hash` prints its contents.

### Method
Built-in

### Endpoint
N/A (Shell Built-in)

### Parameters
#### Path Parameters
N/A

#### Query Parameters
N/A

#### Request Body
N/A

### Request Example
```bash
hash -r
hash -p /usr/bin/vim vim
hash -t ls
```

### Response
#### Success Response (0)
- **status** (integer) - 0 on success, non-zero on failure.
- **output** (string) - The path to the command if `-t` is used.

#### Response Example
```json
{
  "status": 0,
  "output": "/bin/ls"
}
```
```

--------------------------------

### Bash Programmable Completion: Wordlist for Completions (-W)

Source: https://www.gnu.org/software/bash/manual/html_node/Programmable-Completion-Builtins

Splits a wordlist using IFS delimiters and expands each word. Completions are generated from the resulting list that match the prefix of the word being completed. Shell quoting within the wordlist is supported.

```bash
# Example usage:
# compspec -W "apple banana cherry"
```

--------------------------------

### Bash: Suspend shell execution with suspend command

Source: https://www.gnu.org/software/bash/manual/html_node/Job-Control-Builtins

The 'suspend' command pauses the execution of the current shell until it receives a SIGCONT signal. A login shell or a shell without job control cannot be suspended unless the -f option is used to force suspension. The return status is 0 unless the shell is a login shell or job control is not enabled and -f is not supplied.

```bash
suspend [-f]
```

--------------------------------

### Bash Shopt Option: cdable_vars

Source: https://www.gnu.org/software/bash/manual/html_node/The-Shopt-Builtin

With 'cdable_vars' set, an argument to the 'cd' builtin that is not a directory is treated as a variable name whose value is the directory to change to.

```bash
# If this is set, an argument to the `cd` builtin command that is not a directory is assumed to be the name of a variable whose value is the directory to change to.
```

--------------------------------

### Bash Builtin: Continue Command

Source: https://www.gnu.org/software/bash/manual/html_node/Bourne-Shell-Builtins

The 'continue' command resumes the next iteration of an enclosing loop ('for', 'while', 'until', 'select'). An optional argument 'n' specifies which nested loop to continue. It returns a zero status unless 'n' is invalid.

```bash
continue [n]
```

--------------------------------

### Bash 'while' Loop Syntax

Source: https://www.gnu.org/software/bash/manual/html_node/Looping-Constructs

The 'while' loop executes a block of commands as long as a given test command returns a zero exit status. The loop terminates when the test command fails (returns non-zero). The return status is that of the last command in the loop's body.

```bash
while test-commands; do consequent-commands; done
```

--------------------------------

### Bash: Replace Pattern at Beginning

Source: https://www.gnu.org/software/bash/manual/html_node/Shell-Parameter-Expansion

Replaces the pattern if it matches at the beginning of the parameter's expanded value. The replacement string undergoes various expansions.

```bash
${parameter/#pattern/string}
```

--------------------------------

### Enable/Disable Shell Builtin Commands in Bash

Source: https://www.gnu.org/software/bash/manual/html_node/Bash-Builtins

The 'enable' command manages shell builtin commands. It can enable or disable builtins, allowing executables with the same name to be used. It can also list builtins, load new ones from shared objects, and delete loaded builtins. Options control the display and scope of operations.

```bash
enable -n command_name
enable -f /path/to/shared_object command_name
enable -p
enable -a
```

--------------------------------

### Bash: Enable History Substitution with set -H

Source: https://www.gnu.org/software/bash/manual/html_node/The-Set-Builtin

The `set -H` option enables history substitution, allowing users to recall and reuse previous commands using special characters like '!'. This feature is enabled by default for interactive shells.

```bash
# Enable history substitution (usually default for interactive shells)
set -H

# Example: Execute the last command again
!

# Example: Execute a command starting with 'ls'
!ls

# Disable history substitution
set +H
```

--------------------------------

### Bash Parameter Expansion: Error Handling and Conditional Output

Source: https://www.gnu.org/software/bash/manual/html_node/Shell-Parameter-Expansion

Illustrates `${parameter:?word}` for displaying error messages and exiting (or preventing execution in interactive shells) when a parameter is null or unset. It also shows `${parameter:+word}` for substituting a value only when the parameter is set and not null.

```bash
$ var=
$ : ${var:?var is unset or null}
bash: var: var is unset or null
$ echo ${var?var is unset}

$ unset var
$ : ${var?var is unset}
bash: var: var is unset
$ : ${var:?var is unset or null}
bash: var: var is unset or null
$ var=123
$ echo ${var:?var is unset or null}
123

```

```bash
$ var=123
$ echo ${var:+var is set and not null}
var is set and not null
$ echo ${var+var is set}
var is set
$ var=
$ echo ${var:+var is set and not null}

$ echo ${var+var is set}
var is set
$ unset var
$ echo ${var+var is set}

$ echo ${var:+var is set and not null}

$ 

```

--------------------------------

### Bash mapfile: Read Input into Array

Source: https://www.gnu.org/software/bash/manual/html_node/Bash-Builtins

The `mapfile` builtin command reads lines from standard input or a specified file descriptor into an indexed array. It supports options for delimiters, line counts, origin index, discarding lines, removing trailing delimiters, and callback functions for processing lines in chunks.

```bash
mapfile [-d delim] [-n count] [-O origin] [-s count]
    [-t] [-u fd] [-C callback] [-c quantum] [array]

```

--------------------------------

### Bash 'set -n' for Syntax Checking (No Execution)

Source: https://www.gnu.org/software/bash/manual/html_node/The-Set-Builtin

Explains the '-n' option, which reads commands but does not execute them. This is useful for checking scripts for syntax errors without actually running them. It is ignored in interactive shells.

```bash
# Read commands but do not execute them (syntax check)
set -n
```

--------------------------------

### Here Strings in Bash

Source: https://www.gnu.org/software/bash/manual/html_node/Redirections

A variant of here documents where a string is supplied as standard input to a command. The string undergoes various expansions before being provided as input, with a newline appended. The format is `[n]<<< word`.

```bash
[n]<<< word
```

--------------------------------

### Bash Programmable Completion: Glob Pattern for Completions (-G)

Source: https://www.gnu.org/software/bash/manual/html_node/Programmable-Completion-Builtins

Uses a filename expansion pattern (globpat) to generate possible completions. This is a straightforward way to complete files or directories based on a pattern. Shell quoting is honored within the pattern.

```bash
# Example usage:
# compspec -G "*.txt"
```

--------------------------------

### Set File Creation Mask: umask

Source: https://www.gnu.org/software/bash/manual/html_node/Bourne-Shell-Builtins

The `umask` command sets the file creation mask for the process. It can accept an octal number or a symbolic mode. If no mode is provided, it prints the current mask. Options `-p` and `-S` control the output format.

```bash
umask [-p] [-S] [mode]
```

--------------------------------

### Bash Pipeline Syntax

Source: https://www.gnu.org/software/bash/manual/html_node/Pipelines

Defines the general syntax for a Bash pipeline, which can include optional timing information and a negation operator.

```bash
[time [-p]] [!] command1 [ | or |& command2 ] ...
```

--------------------------------

### Bash Pipeline Timing

Source: https://www.gnu.org/software/bash/manual/html_node/Pipelines

Shows how to use the 'time' reserved word to measure the execution time of a Bash pipeline. The '-p' option formats the output according to POSIX standards.

```bash
time pipeline_command
```

```bash
time -p pipeline_command
```

--------------------------------

### Display Trap Commands with trap -p

Source: https://www.gnu.org/software/bash/manual/html_node/Bourne-Shell-Builtins

The `trap -p` command displays the trap commands associated with signals. If no sigspecs are provided, it shows traps for all signals. This output can be reused to restore signal dispositions. The `-P` option is similar but only shows actions for specified sigspecs and requires at least one sigspec argument. These options can be used in subshells to inspect parent shell traps.

```bash
trap -p [sigspec ...]
```

```bash
trap -P [sigspec ...]
```

--------------------------------

### Bash: Compound Command Operators

Source: https://www.gnu.org/software/bash/manual/html_node/Conditional-Constructs

Illustrates the use of compound command operators in Bash for controlling program flow and expression evaluation. It covers grouping, negation, logical AND, and logical OR.

```bash
( expression )
! expression
expression1 && expression2
expression1 || expression2
```

--------------------------------

### Command that returns a non-zero status

Source: https://www.gnu.org/software/bash/manual/html_node/Bourne-Shell-Builtins

The `false` command performs no action and always returns a non-zero exit status, indicating failure. It is often used in scripting for conditional logic where a failure state is required.

```bash
false
```

--------------------------------

### List Signal Names and Numbers with trap -l

Source: https://www.gnu.org/software/bash/manual/html_node/Bourne-Shell-Builtins

The `trap -l` command prints a list of signal names and their corresponding numbers. If no sigspec arguments are given, it lists all valid signal names. Signal names are case-insensitive and the 'SIG' prefix is optional.

```bash
trap -l [sigspec ...]
```

--------------------------------

### Bash 'set -h' for Command Hashing

Source: https://www.gnu.org/software/bash/manual/html_node/The-Set-Builtin

Explains the '-h' option, which enables command hashing. This feature optimizes command lookup by remembering the locations of executed commands, and it is enabled by default in Bash.

```bash
# Enable command hashing (remembering command locations)
set -h
```

--------------------------------

### Display User and System Times with 'times' in Bash

Source: https://www.gnu.org/software/bash/manual/html_node/Bourne-Shell-Builtins

The 'times' builtin command prints out the user and system times used by the current shell and any processes it has spawned. The command returns a zero exit status, indicating success. It does not take any arguments.

```bash
# Display the times used by the shell and its children
times
```

--------------------------------

### Bash 'for' Loop Syntax (C-Style Arithmetic)

Source: https://www.gnu.org/software/bash/manual/html_node/Looping-Constructs

An alternative 'for' loop construct similar to C, which evaluates arithmetic expressions. It initializes, checks a condition, and increments/decrements in a manner analogous to C's for loop.

```bash
for (( expr1 ; expr2 ; expr3 )) [;] do commands ; done
```

--------------------------------

### Bash Programmable Completion: Execute Function for Completions (-F)

Source: https://www.gnu.org/software/bash/manual/html_node/Programmable-Completion-Builtins

Defines a shell function to be executed for generating completions. The function receives the current command, word being completed, and preceding word as arguments. Completions are stored in the COMPREPLY array. This allows for complex, context-aware completion logic.

```bash
# Example function definition:
_my_completion_func() {
  local cur=${COMP_WORDS[COMP_CWORD]}
  COMPREPLY=( $(compgen -W "option1 option2" -- "$cur") )
}

# Register the function for a command:
# complete -F _my_completion_func mycommand
```

--------------------------------

### Bash 'until' Loop Syntax

Source: https://www.gnu.org/software/bash/manual/html_node/Looping-Constructs

The 'until' loop executes a block of commands as long as a given test command returns a non-zero exit status. The loop terminates when the test command succeeds (returns zero). The return status is that of the last command in the loop's body.

```bash
until test-commands; do consequent-commands; done
```

--------------------------------

### Bash: Control Symbolic Link Resolution with set -P

Source: https://www.gnu.org/software/bash/manual/html_node/The-Set-Builtin

The `set -P` option in Bash prevents the shell from resolving symbolic links when executing commands that change the current directory, such as `cd`. This ensures that directory operations follow the physical directory structure rather than the logical one. By default, Bash follows symbolic links.

```bash
if set -P;
then
    echo "Symbolic link resolution is disabled."
else
    echo "Symbolic link resolution is enabled."
fi
```

--------------------------------

### Bash read Command for Input Processing

Source: https://www.gnu.org/software/bash/manual/html_node/Bash-Builtins

The `read` command in Bash reads a line from standard input or a file descriptor, splitting it into words based on IFS. It assigns these words to specified names, with options for array assignment, custom delimiters, and Readline integration.

```bash
read -p "Enter your name: " name
```

```bash
read -a colors -d ',' "red,green,blue"
```

--------------------------------

### exec

Source: https://www.gnu.org/software/bash/manual/html_node/Bourne-Shell-Builtins

Replaces the shell with a command, or modifies the current shell environment through redirections. It can execute a command without creating a new process or set up redirections.

```APIDOC
## exec

### Description
If `command` is supplied, it replaces the shell without creating a new process. The arguments become the arguments to `command`. The `-l` option prepends a dash to the zeroth argument, similar to the `login` program. The `-c` option executes `command` with an empty environment. The `-a` option passes `name` as the zeroth argument to `command`. If `command` cannot be executed, a non-interactive shell exits unless `execfail` is enabled, in which case it returns a non-zero status. An interactive shell returns a non-zero status if the file cannot be executed. A subshell exits unconditionally if `exec` fails. If `command` is not specified, redirections can be used to affect the current shell environment. The return status is zero if there are no redirection errors, otherwise non-zero.

### Method
Built-in

### Endpoint
N/A (Shell Built-in)

### Parameters
#### Path Parameters
N/A

#### Query Parameters
N/A

#### Request Body
N/A

### Request Example
```bash
exec ls -l
exec > output.txt
```

### Response
#### Success Response (0)
- **status** (integer) - 0 on success, non-zero on failure.

#### Response Example
```json
{
  "status": 0
}
```
```

--------------------------------

### Shopt Builtin Command

Source: https://www.gnu.org/software/bash/manual/html_node/The-Shopt-Builtin

The `shopt` builtin command is used to change additional optional shell behavior. It can be used to enable or disable various shell options that affect how Bash operates.

```APIDOC
## Shopt Builtin Command

### Description
Allows modification of optional shell behavior through various settings.

### Method
Builtin Command

### Endpoint
N/A (Shell Builtin)

### Parameters
#### Options
- `-p` (boolean) - Display a list of all settable options, with an indication of whether or not each is set. Output may be reused as input.
- `-s` (boolean) - Enable each optname.
- `-u` (boolean) - Disable each optname.
- `-q` (boolean) - Suppresses normal output; the return status indicates whether the optname is set or unset.
- `-o` (boolean) - Restricts the values of optname to be those defined for the `-o` option to the `set` builtin.

#### Optnames
- `array_expand_once` (boolean) - Suppresses multiple evaluation of associative and indexed array subscripts.
- `assoc_expand_once` (boolean) - Deprecated; a synonym for `array_expand_once`.
- `autocd` (boolean) - If set, a command name that is the name of a directory is executed as if it were the argument to the `cd` command.
- `bash_source_fullpath` (boolean) - If set, filenames added to the `BASH_SOURCE` array variable are converted to full pathnames.
- `cdable_vars` (boolean) - If set, an argument to the `cd` builtin command that is not a directory is assumed to be the name of a variable whose value is the directory to change to.
- `cdspell` (boolean) - If set, the `cd` command attempts to correct minor errors in the spelling of a directory component.
- `checkhash` (boolean) - If set, Bash checks that a command found in the hash table exists before trying to execute it.
- `checkjobs` (boolean) - If set, Bash lists the status of any stopped and running jobs before exiting an interactive shell.
- `checkwinsize` (boolean) - If set, Bash checks the window size after each external command and updates `LINES` and `COLUMNS`.
- `cmdhist` (boolean) - If set, Bash attempts to save all lines of a multiple-line command in the same history entry.
- `compat31` to `compat44` (boolean) - Control aspects of the shell’s compatibility mode.
- `complete_fullquote` (boolean) - If set, Bash quotes all shell metacharacters in filenames and directory names when performing completion.
- `direxpand` (boolean) - Controls directory expansion behavior.

### Request Example
```bash
shopt -s autocd
shopt -p autocd
```

### Response
#### Success Response (0)
- `optname` (string) - The name of the shell option.
- `status` (boolean) - Indicates if the option is set or unset.

#### Response Example
```
autocd
```

#### Error Response (non-zero)
- `error` (string) - Description of the error, e.g., invalid option name.
```

--------------------------------

### Bash 'set -e' for Exiting on Error

Source: https://www.gnu.org/software/bash/manual/html_node/The-Set-Builtin

Illustrates the '-e' option, which causes the shell to exit immediately if a command returns a non-zero status. This is crucial for script robustness, though it has exceptions for certain command structures and ignored contexts.

```bash
# Exit immediately if a command exits with a non-zero status
set -e
```

--------------------------------

### Execute Command on Function Return with trap RETURN

Source: https://www.gnu.org/software/bash/manual/html_node/Bourne-Shell-Builtins

The `trap RETURN` command executes an action each time a shell function or a script executed with '.' or 'source' finishes. This trap is useful for performing actions after a function or sourced script has completed its execution.

```bash
trap 'action' RETURN
```

--------------------------------

### Bash: Inherit Traps with set -E and set -T

Source: https://www.gnu.org/software/bash/manual/html_node/The-Set-Builtin

The `set -E` option ensures that `ERR` traps are inherited by shell functions, command substitutions, and subshells. Similarly, `set -T` ensures that `DEBUG` and `RETURN` traps are inherited. These options are crucial for consistent error handling and debugging across different execution contexts.

```bash
# Enable inheritance of ERR trap
set -E

# Enable inheritance of DEBUG and RETURN traps
set -T

# Define a trap
trap 'echo "An error occurred!"' ERR

# Function that might trigger the trap
my_function() {
  ls non_existent_file
}

# Call the function
my_function
```

--------------------------------

### Bash 'for' Loop Syntax (List Expansion)

Source: https://www.gnu.org/software/bash/manual/html_node/Looping-Constructs

The standard 'for' loop iterates over a list of words. For each word in the expanded list, the loop body is executed with a variable assigned to the current word. If no list is provided, it iterates over positional parameters.

```bash
for name [ [in words ...] ; ] do commands; done
```

--------------------------------

### GFDL Notice with Invariant Sections, Cover Texts

Source: https://www.gnu.org/software/bash/manual/html_node/GNU-Free-Documentation-License

This alternative notice is for documents licensed under the GFDL that include Invariant Sections, Front-Cover Texts, and Back-Cover Texts. It modifies the standard notice to specify the titles of invariant sections and the content of cover texts.

```text
    with the Invariant Sections being list their titles, with
    the Front-Cover Texts being list, and with the Back-Cover Texts
    being list.

```

--------------------------------

### Manage Signal Traps with 'trap' in Bash

Source: https://www.gnu.org/software/bash/manual/html_node/Bourne-Shell-Builtins

The 'trap' builtin command allows you to specify shell commands to be executed when the shell receives specific signals. You can set actions for signals, reset signal dispositions, or ignore signals. If no arguments are provided, 'trap' prints the current signal trap settings.

```bash
# Execute 'cleanup.sh' when the shell receives SIGINT (Ctrl+C)
trap './cleanup.sh' SIGINT

# Ignore the SIGHUP signal
trap '' HUP

# Reset the disposition of SIGTERM to its default
trap - TERM

# Print current trap settings
trap -p

# Execute a command when EXIT signal is received (e.g., on script termination)
trap 'echo "Script finished."' EXIT
```

--------------------------------

### Bash Shopt Option: autocd

Source: https://www.gnu.org/software/bash/manual/html_node/The-Shopt-Builtin

If 'autocd' is set, a command name that is the name of a directory is executed as if it were the argument to the 'cd' command. This option is primarily for interactive shells.

```bash
# If set, a command name that is the name of a directory is executed as if it were the argument to the `cd` command. This option is only used by interactive shells.
```

--------------------------------

### Bash Builtin: Period (.) Command (Source)

Source: https://www.gnu.org/software/bash/manual/html_node/Bourne-Shell-Builtins

The period builtin command, equivalent to 'source', reads and executes commands from a specified filename within the current shell context. It searches for the file in directories specified by PATH or CDPATH. Arguments provided become positional parameters for the executed commands.

```bash
. [-p path] filename [arguments]
```

--------------------------------

### Bash Pipeline with Negation

Source: https://www.gnu.org/software/bash/manual/html_node/Pipelines

Demonstrates how to negate the exit status of a Bash pipeline using the '!' operator. The pipeline's final exit status will be inverted.

```bash
! pipeline_command
```

--------------------------------

### No-op command: true

Source: https://www.gnu.org/software/bash/manual/html_node/Bourne-Shell-Builtins

The `true` command does nothing and always returns a status of 0. It is often used in scripts as a placeholder or to ensure a command in a conditional statement always succeeds.

```bash
true
```

--------------------------------

### Bash Shopt Option: complete_fullquote

Source: https://www.gnu.org/software/bash/manual/html_node/The-Shopt-Builtin

If 'complete_fullquote' is set, Bash quotes all shell metacharacters in filenames during completion. This behavior is the default for Bash versions up to 4.2.

```bash
# If set, Bash quotes all shell metacharacters in filenames and directory names when performing completion. If not set, Bash removes metacharacters such as the dollar sign from the set of characters that will be quoted in completed filenames when these metacharacters appear in shell variable references in words to be completed. This means that dollar signs in variable names that expand to directories will not be quoted; however, any dollar signs appearing in filenames will not be quoted, either. This is active only when Bash is using backslashes to quote completed filenames. This variable is set by default, which is the default Bash behavior in versions through 4.2.
```

--------------------------------

### Bash local: Create Function-Scoped Variables

Source: https://www.gnu.org/software/bash/manual/html_node/Bash-Builtins

The `local` builtin command creates variables with a scope restricted to the current function and its children. It accepts options similar to `declare`. Using `local` outside a function or with invalid arguments results in an error. It can also manage shell options locally.

```bash
local [option] name[=value] ...

```

--------------------------------

### export

Source: https://www.gnu.org/software/bash/manual/html_node/Bourne-Shell-Builtins

Marks shell variables or functions to be passed to the environment of subsequently executed commands. It can also display exported variables or functions.

```APIDOC
## export [-fn] [-p] [name[=value]]

### Description
Mark each `name` to be passed to subsequently executed commands in the environment. If the `-f` option is supplied, the names refer to shell functions; otherwise, they refer to shell variables. The `-n` option means to unexport each name. If no names are supplied, or if only the `-p` option is given, `export` displays a list of names of all exported variables. Using `-p` and `-f` together displays exported functions. The `-p` option displays output in a form that may be reused as input. `export` allows the value of a variable to be set at the same time it is exported or unexported by following the variable name with `=value`. The return status is zero unless an invalid option is supplied, one of the names is not a valid shell variable name, or `-f` is supplied with a name that is not a shell function.

### Method
Built-in

### Endpoint
N/A (Shell Built-in)

### Parameters
#### Path Parameters
N/A

#### Query Parameters
N/A

#### Request Body
N/A

### Request Example
```bash
export MY_VAR="some_value"
export -p
export -f my_function
```

### Response
#### Success Response (0)
- **status** (integer) - 0 on success, non-zero on failure.
- **output** (string) - List of exported variables or functions when using `-p`.

#### Response Example
```json
{
  "status": 0,
  "output": "declare -x MY_VAR=\"some_value\""
}
```
```

--------------------------------

### Evaluate Conditional Expressions with 'test' and '[' in Bash

Source: https://www.gnu.org/software/bash/manual/html_node/Bourne-Shell-Builtins

The 'test' and '[' builtins evaluate conditional expressions. They return a status of 0 (true) or 1 (false). Each operator and operand must be a separate argument. The 'test' command does not accept options, and '--' is not recognized as an end-of-options marker. When using the '[' form, the last argument must be ']'. The evaluation rules depend on the number of arguments provided.

```bash
# Example of using 'test' for string comparison
test -n "string1"

# Example of using '[' for string comparison
[ -n "string1" ]

# Example of combining conditions using '&&' (preferred over '-a')
test -n "string1" && test -n "string2"

# Example of combining conditions using '||' (preferred over '-o')
test -f "file1" || test -f "file2"

# Example of checking if a file exists
if test -f "myfile.txt"; then
  echo "File exists."
fi

# Example of checking if a string is not empty
if [ -n "$MY_VAR" ]; then
  echo "MY_VAR is not empty."
fi

# Example of checking if two strings are equal
if [ "$STR1" = "$STR2" ]; then
  echo "Strings are equal."
fi

# Example of checking if a number is less than another
if [ "$NUM1" -lt "$NUM2" ]; then
  echo "NUM1 is less than NUM2."
fi

# Example of grouping expressions to override precedence
if ( test -f "file1" || test -f "file2" ) && test -w "file3"; then
  echo "Either file1 or file2 exists, and file3 is writable."
fi
```

--------------------------------

### Bash `compopt` Builtin: Modify Completion Options

Source: https://www.gnu.org/software/bash/manual/html_node/Programmable-Completion-Builtins

Modifies completion options for specified names or for the current completion if no names are given. Options like -o, -D, -E, and -I control various aspects of completion behavior, including default and empty completions. If no options are supplied, it displays current settings.

```bash
# Example usage:
# compopt -o nospace mycommand  # Disable space insertion after completion
# compopt -D -o default mycommand # Apply default options to command completion
# compopt mycommand             # Display options for mycommand
```

--------------------------------

### Bash printf: Formatted Output

Source: https://www.gnu.org/software/bash/manual/html_node/Bash-Builtins

The `printf` builtin command writes formatted arguments to standard output or assigns them to a variable using the `-v` option. It supports standard `printf(3)` format specifiers and additional ones like `%b` for backslash escape expansion and `%q` or `%Q` for shell-reusable or ANSI-C quoted output.

```bash
printf [-v var] format [arguments]

```

--------------------------------

### Append Redirected Output in Bash

Source: https://www.gnu.org/software/bash/manual/html_node/Redirections

Appends redirected output to a file. If the file does not exist, it is created. The format is `[n]>>word`, where `n` is the file descriptor (defaulting to 1 for standard output) and `word` is the filename.

```bash
[n]>>word
```

--------------------------------

### Bash Programmable Completion: Filter Completions (-X)

Source: https://www.gnu.org/software/bash/manual/html_node/Programmable-Completion-Builtins

Filters the list of possible completions using a pattern. Matches are removed from the list. A leading '!' negates the pattern, removing completions that do *not* match. This allows for fine-grained control over the final completion set.

```bash
# Example usage:
# compspec -X "*.tmp"  # Remove .tmp files
# compspec -X "!*.log" # Keep only .log files
```

--------------------------------

### Hash Command in Bash

Source: https://www.gnu.org/software/bash/manual/html_node/Bourne-Shell-Builtins

The `hash` command in Bash remembers the full filenames of commands to speed up subsequent invocations. It searches directories in the `$PATH` environment variable. Options like -p, -r, -d, -t, and -l modify its behavior regarding path searching, forgetting remembered locations, and output formatting.

```bash
hash [-p filename] [-r] [-d name ...] [-t name ...] [name ...]
```

--------------------------------

### Redirect Standard Output and Error in Bash

Source: https://www.gnu.org/software/bash/manual/html_node/Redirections

Redirects both standard output (file descriptor 1) and standard error (file descriptor 2) to a specified file. The preferred format is `&>word`, which is equivalent to `>word 2>&1`.

```bash
&>word
```

```bash
>&word
```

```bash
>word 2>&1
```

--------------------------------

### Bash read Command for Fixed Character or Delimited Input

Source: https://www.gnu.org/software/bash/manual/html_node/Bash-Builtins

The `-n nchars` option makes `read` return after reading a specified number of characters, respecting EOF or timeouts. The `-N nchars` option reads exactly `nchars` characters, not treating delimiters specially. The `-d delim` option specifies a custom line terminator.

```bash
read -n 5 -t 2 "input_buffer"
```

```bash
read -N 10 -r "exact_chars"
```

```bash
read -d ':' "field"
```

--------------------------------

### Bash: Pattern Matching with [[ == and != ]]

Source: https://www.gnu.org/software/bash/manual/html_node/Conditional-Constructs

Illustrates pattern matching using the == and != operators within Bash's [[ ... ]] construct. The string to the right of the operator is treated as a pattern. The nocasematch shell option can be enabled for case-insensitive matching. Quoting any part of the pattern results in literal matching.

```bash
[[ "$string" == "pattern" ]]

```

```bash
[[ "$string" != "pattern" ]]

```

--------------------------------

### Bash Builtin: Eval Command

Source: https://www.gnu.org/software/bash/manual/html_node/Bourne-Shell-Builtins

The 'eval' command concatenates its arguments into a single command string, which Bash then reads and executes. The exit status of 'eval' is the exit status of the executed command. It returns zero if no arguments are provided or if only empty arguments are given.

```bash
eval [arguments]
```

--------------------------------

### Bash Long Options for Invocation

Source: https://www.gnu.org/software/bash/manual/html_node/Invoking-Bash

Lists and describes the long options available when invoking Bash. These options control features like debugging, internationalization string extraction, initialization file loading, and shell behavior.

```bash
--debugger
    Arrange for the debugger profile to be executed before the shell starts. Turns on extended debugging mode.
```

```bash
--dump-po-strings
    Print a list of all double-quoted strings preceded by ‘$’ on the standard output in the GNU `gettext` PO (portable object) file format.
```

```bash
--dump-strings
    Equivalent to -D.
```

```bash
--help
    Display a usage message on standard output and exit successfully.
```

```bash
--init-file filename
--rcfile filename
    Execute commands from filename (instead of ~/.bashrc) in an interactive shell.
```

```bash
--login
    Equivalent to -l.
```

```bash
--noediting
    Do not use the GNU Readline library to read command lines when the shell is interactive.
```

```bash
--noprofile
    Don’t load the system-wide startup file /etc/profile or any of the personal initialization files ~/.bash_profile, ~/.bash_login, or ~/.profile when Bash is invoked as a login shell.
```

```bash
--norc
    Don’t read the ~/.bashrc initialization file in an interactive shell.
```

```bash
--posix
    Enable POSIX mode; change the behavior of Bash where the default operation differs from the POSIX standard to match the standard.
```

```bash
--restricted
    Equivalent to -r. Make the shell a restricted shell.
```

```bash
--verbose
    Equivalent to -v. Print shell input lines as they’re read.
```

```bash
--version
    Show version information for this instance of Bash on the standard output and exit successfully.
```

--------------------------------

### Return from Shell Function or Sourced File in Bash

Source: https://www.gnu.org/software/bash/manual/html_node/Bourne-Shell-Builtins

The `return` command terminates the execution of a shell function or a sourced script, returning an exit status to the caller. If an argument `n` is provided, it's used as the return value; otherwise, the exit status of the last command is used. It can also be affected by trap handlers.

```bash
return [n]
```

--------------------------------

### false

Source: https://www.gnu.org/software/bash/manual/html_node/Bourne-Shell-Builtins

A command that does nothing and returns a non-zero status, typically used in conditional logic to force a false outcome.

```APIDOC
## false

### Description
Does nothing; returns a non-zero status.

### Method
Built-in

### Endpoint
N/A (Shell Built-in)

### Parameters
#### Path Parameters
N/A

#### Query Parameters
N/A

#### Request Body
N/A

### Request Example
```bash
false
```

### Response
#### Success Response (non-zero)
- **status** (integer) - A non-zero exit status.

#### Response Example
```json
{
  "status": 1
}
```
```

--------------------------------

### Append Standard Output and Error in Bash

Source: https://www.gnu.org/software/bash/manual/html_node/Redirections

Appends both standard output (file descriptor 1) and standard error (file descriptor 2) to a specified file. The format is `&>>word`, which is equivalent to `>>word 2>&1`.

```bash
&>>word
```

```bash
>>word 2>&1
```

--------------------------------

### Bash Shopt Option: cmdhist

Source: https://www.gnu.org/software/bash/manual/html_node/The-Shopt-Builtin

When 'cmdhist' is set, Bash saves multi-line commands in a single history entry, facilitating easier re-editing. This option requires command history to be enabled.

```bash
# If set, Bash attempts to save all lines of a multiple-line command in the same history entry. This allows easy re-editing of multi-line commands. This option is enabled by default, but only has an effect if command history is enabled (see Bash History Facilities).
```

--------------------------------

### Bash Builtin: Break Command

Source: https://www.gnu.org/software/bash/manual/html_node/Bourne-Shell-Builtins

The 'break' command is used to exit from enclosing 'for', 'while', 'until', or 'select' loops. An optional argument 'n' specifies the number of nested loops to exit. The command returns a zero status unless 'n' is invalid.

```bash
break [n]
```

--------------------------------

### Print Working Directory (pwd) in Bash

Source: https://www.gnu.org/software/bash/manual/html_node/Bourne-Shell-Builtins

The `pwd` command prints the absolute pathname of the current working directory. It accepts options -L and -P to control whether symbolic links are included in the output. The -P option (or `set -o physical`) ensures that symbolic links are not resolved.

```bash
pwd [-LP]
```

--------------------------------

### Bash Shopt Option: cdspell

Source: https://www.gnu.org/software/bash/manual/html_node/The-Shopt-Builtin

The 'cdspell' option allows the 'cd' command to attempt corrections for minor spelling errors in directory names, such as transposed or missing characters. This is for interactive shells.

```bash
# If set, the `cd` command attempts to correct minor errors in the spelling of a directory component. Minor errors include transposed characters, a missing character, and one extra character. If `cd` corrects the directory name, it prints the corrected filename, and the command proceeds. This option is only used by interactive shells.
```

--------------------------------

### Declare Variables and Attributes in Bash

Source: https://www.gnu.org/software/bash/manual/html_node/Bash-Builtins

The 'declare' command in Bash is used to manage shell variables and their attributes. It can set variable types (like arrays), make them read-only, export them, or make them local within functions. It also handles variable assignment and provides return status codes for various error conditions.

```bash
declare -x VARIABLE_NAME=value
declare -r READONLY_VAR=value
declare -a ARRAY_VAR
declare -A ASSOCIATIVE_ARRAY
local MY_VAR=value
```

--------------------------------

### Execute Command on Shell Exit with trap

Source: https://www.gnu.org/software/bash/manual/html_node/Bourne-Shell-Builtins

The `trap` command can execute an action when the shell exits. This is achieved by specifying '0' or 'EXIT' as the sigspec. This allows for cleanup operations or final tasks before the shell terminates.

```bash
trap 'action' 0
```

```bash
trap 'action' EXIT
```

--------------------------------

### Display Directory Stack (Bash)

Source: https://www.gnu.org/software/bash/manual/html_node/Directory-Stack-Builtins

The `dirs` command displays the list of currently remembered directories in the directory stack. Options control the output format, such as clearing the stack, using full pathnames, or printing entries with their indices.

```bash
dirs [-clpv] [+N | -N]
```

--------------------------------

### Bash Builtin: Change Directory (cd) Command

Source: https://www.gnu.org/software/bash/manual/html_node/Bourne-Shell-Builtins

The 'cd' command changes the current working directory. It supports options for handling symbolic links (-L, -P) and searching through CDPATH. If no directory is specified, it defaults to the HOME variable. It updates PWD and OLDPWD environment variables and returns a zero status on success.

```bash
cd [-L] [-@] [directory]
cd -P [-e] [-@] [directory]
```

--------------------------------

### Add/Rotate Directories in Stack (Bash)

Source: https://www.gnu.org/software/bash/manual/html_node/Directory-Stack-Builtins

The `pushd` command adds a directory to the top of the directory stack or rotates the stack. Without arguments, it exchanges the top two elements. Options allow for suppressing directory changes or rotating the stack to bring a specific directory to the top.

```bash
pushd [-n] [+N | -N | dir]
```

--------------------------------

### Standard Command Substitution in Bash

Source: https://www.gnu.org/software/bash/manual/html_node/Command-Substitution

Allows the output of a command to replace the command itself. Bash executes the command in a subshell and replaces the substitution with its standard output, removing trailing newlines. Embedded newlines may be removed during word splitting.

```bash
echo $(ls -l)

```

```bash
echo `date`

```

```bash
echo $(< file.txt)

```

--------------------------------

### Bash: Regular Expression Matching with [[ =~ ]]

Source: https://www.gnu.org/software/bash/manual/html_node/Conditional-Constructs

Demonstrates using the =~ operator within Bash's [[ ... ]] construct for POSIX extended regular expression matching. This allows for complex pattern matching on strings. The match is case-insensitive if the nocasematch shell option is enabled. Quoting parts of the pattern can force literal matching.

```bash
[[ $line =~ [[:space:]]*(a)?b ]]

```

```bash
[[ $line =~ ^"initial string" ]]

```

```bash
pattern='[[:space:]]*(a)?b'
[[ $line =~ $pattern ]]

```

--------------------------------

### Bash history Command: History Management

Source: https://www.gnu.org/software/bash/manual/html_node/Bash-History-Builtins

The 'history' command in Bash displays and manages the command history list. It supports various options for clearing, deleting, appending, reading, and writing history entries to a file. It also allows for history substitution and time formatting.

```bash
history [n]
history -c
history -d offset
history -d start-end
history [-anrw] [filename]
history -ps arg
```

--------------------------------

### Bash: Print Shell Input Lines with set -v

Source: https://www.gnu.org/software/bash/manual/html_node/The-Set-Builtin

The `set -v` option, also known as `verbose`, causes Bash to print shell input lines to standard error as they are read. This option is useful for understanding the flow of script execution and identifying where input is being processed.

```bash
# Enable verbose mode
set -v

echo "Hello, world!"

# Disable verbose mode
set +v
```

--------------------------------

### Bash 'set -f' to Disable Filename Expansion (Globbing)

Source: https://www.gnu.org/software/bash/manual/html_node/The-Set-Builtin

Shows how to use the '-f' option to disable filename expansion, commonly known as globbing. This prevents characters like '*', '?', and '[]' from being interpreted as wildcards.

```bash
# Disable filename expansion (globbing)
set -f
```

--------------------------------

### Bash: Replace All Pattern Matches

Source: https://www.gnu.org/software/bash/manual/html_node/Shell-Parameter-Expansion

Replaces all occurrences of a pattern in a parameter's expanded value with a specified string. The replacement string undergoes various expansions.

```bash
${parameter//pattern/string}
```

--------------------------------

### Bash Shopt Option: checkjobs

Source: https://www.gnu.org/software/bash/manual/html_node/The-Shopt-Builtin

If 'checkjobs' is enabled, Bash displays the status of stopped and running jobs before exiting an interactive shell. It defers exiting if jobs are running or stopped.

```bash
# If set, Bash lists the status of any stopped and running jobs before exiting an interactive shell. If any jobs are running, Bash defers the exit until a second exit is attempted without an intervening command (see Job Control). The shell always postpones exiting if any jobs are stopped.
```

--------------------------------

### Compound Assignment with Alternating Keys and Values for Associative Array in Bash

Source: https://www.gnu.org/software/bash/manual/html_node/Arrays

Assigns key-value pairs to an associative array by listing keys and values alternately. This is a shorthand for the explicit key=value syntax.

```bash
my_assoc_array=(key1 value1 key2 value2)
```

--------------------------------

### Alternate Command Substitution in Bash

Source: https://www.gnu.org/software/bash/manual/html_node/Command-Substitution

Executes a command in the current execution environment and captures its output, with trailing newlines removed. Side effects persist in the current environment. Local variables can be created within this construct.

```bash
${ local X=12345 ; echo $X; }

```

```bash
${| REPLY=12345; }

```

--------------------------------

### Mark variables or functions for environment export

Source: https://www.gnu.org/software/bash/manual/html_node/Bourne-Shell-Builtins

The `export` command marks shell variables or functions to be passed to subsequently executed commands. Options control whether to export variables (`-f`), unexport them (`-n`), or display exported items (`-p`). Variables can be assigned a value during export.

```bash
export [-fn] [-p] [name[=value]]
```

--------------------------------

### Bash logout: Exit Login Shell

Source: https://www.gnu.org/software/bash/manual/html_node/Bash-Builtins

The `logout` builtin command is used to exit a login shell. It returns a specified status code `n` to the parent shell. If no argument is provided, it typically returns 0.

```bash
logout [n]

```

--------------------------------

### Test Expressions in Bash

Source: https://www.gnu.org/software/bash/manual/html_node/Bourne-Shell-Builtins

The `test` command (often used via the `[` alias) evaluates conditional expressions. It returns an exit status of 0 if the expression is true, and non-zero otherwise. This is commonly used in shell scripting for conditional logic.

```bash
test expr
```

```bash
[ expr ]
```

--------------------------------

### Bash: Replace First Pattern Match

Source: https://www.gnu.org/software/bash/manual/html_node/Shell-Parameter-Expansion

Replaces the first occurrence of a pattern in a parameter's expanded value with a specified string. The replacement string undergoes various expansions.

```bash
${parameter/pattern/string}
```

--------------------------------

### exit

Source: https://www.gnu.org/software/bash/manual/html_node/Bourne-Shell-Builtins

Exits the current shell, returning a specified status code to the parent process. If no status is given, it returns the status of the last command executed.

```APIDOC
## exit [n]

### Description
Exit the shell, returning a status of `n` to the shell’s parent. If `n` is omitted, the exit status is that of the last command executed. Any trap on `EXIT` is executed before the shell terminates.

### Method
Built-in

### Endpoint
N/A (Shell Built-in)

### Parameters
#### Path Parameters
N/A

#### Query Parameters
N/A

#### Request Body
N/A

### Request Example
```bash
exit 0
exit
```

### Response
#### Success Response (0)
- **status** (integer) - The exit status code.

#### Response Example
```json
{
  "status": 0
}
```
```

--------------------------------

### Bash Single-Character Options for Invocation

Source: https://www.gnu.org/software/bash/manual/html_node/Invoking-Bash

Details the single-character options that can be used when invoking Bash. These options control aspects like command execution from a string, interactive mode, login shell behavior, restricted mode, and input source.

```bash
-c string
    Read and execute commands from the first non-option argument command_string, then exit. If there are arguments after the command_string, the first argument is assigned to `$0` and any remaining arguments are assigned to the positional parameters.
```

```bash
-i
    Force the shell to run interactively.
```

```bash
-l
    Make this shell act as if it had been directly invoked by login. When the shell is interactive, this is equivalent to starting a login shell with ‘exec -l bash’.
```

```bash
-r
    Make the shell a restricted shell.
```

```bash
-s
    If this option is present, or if no arguments remain after option processing, then Bash reads commands from the standard input.
```

```bash
-D
    Print a list of all double-quoted strings preceded by ‘$’ on the standard output. This implies the -n option; no commands will be executed.
```

```bash
[-+]O [shopt_option]
    shopt_option is one of the shell options accepted by the `shopt` builtin. If shopt_option is present, -O sets the value of that option; +O unsets it.
```

```bash
--
    A `--` signals the end of options and disables further option processing. Any arguments after the `--` are treated as a shell script filename and arguments passed to that script.
```

```bash
-
    Equivalent to `--`.
```

--------------------------------

### Bash TIMEFORMAT Default Value

Source: https://www.gnu.org/software/bash/manual/html_node/Bash-Variables

This snippet shows the default format string used by the `time` reserved word in Bash when the TIMEFORMAT variable is not explicitly set. It defines how pipeline execution times are displayed, including real, user, and system CPU times.

```bash
$'\nreal\t%3lR\nuser\t%3lU\nsys\t%3lS'
```

--------------------------------

### Bash if Statement Syntax

Source: https://www.gnu.org/software/bash/manual/html_node/Conditional-Constructs

The `if` command in Bash allows for conditional execution of commands. It tests a command's exit status and executes subsequent commands based on whether the test is successful (exit status 0) or not. It supports `elif` and `else` for multiple conditions.

```bash
if test-commands; then
  consequent-commands;
[elif more-test-commands; then
  more-consequents;]
[else alternate-consequents;]
fi

```

--------------------------------

### Bash Pipeline with Standard Error Redirection

Source: https://www.gnu.org/software/bash/manual/html_node/Pipelines

Illustrates the use of '|&' in a Bash pipeline, which redirects both standard output and standard error of the preceding command to the standard input of the next command.

```bash
command1 |& command2
```

--------------------------------

### Bash: Transform Parameter Value with Operators

Source: https://www.gnu.org/software/bash/manual/html_node/Shell-Parameter-Expansion

This expansion transforms the value of a parameter or provides information about it, depending on the operator. Operators include case conversion ('U', 'u', 'L'), quoting ('Q'), escape sequence expansion ('E'), prompt expansion ('P'), assignment statement generation ('A'), array key-value pair formatting ('K', 'k'), and attribute flag retrieval ('a').

```Bash
`${parameter@U}`
`${parameter@u}`
`${parameter@L}`
`${parameter@Q}`
`${parameter@E}`
`${parameter@P}`
`${parameter@A}`
`${parameter@K}`
`${parameter@a}`
`${parameter@k}`
```

--------------------------------

### Bash Shell Function Declaration Syntax

Source: https://www.gnu.org/software/bash/manual/html_node/Shell-Functions

Defines the syntax for declaring shell functions in Bash. It shows two common ways to define a function named 'fname'. The `function` keyword is optional, and if used, the parentheses are also optional. The body of the function is a compound command, typically enclosed in curly braces.

```bash
fname () compound-command [ redirections ]
```

```bash
function fname [()] compound-command [ redirections ]
```

--------------------------------

### Manage command hash table

Source: https://www.gnu.org/software/bash/manual/html_node/Bourne-Shell-Builtins

The `hash` command manipulates the shell's command hash table, which stores the locations of previously executed commands for faster lookup. Options allow resetting the table (`-r`), specifying a filename (`-p`), or displaying table contents (`-d`, `-t`).

```bash
hash [-r] [-p filename] [-dt] [name]
```

--------------------------------

### Execute Commands in Current Shell with Curly Braces {} in Bash

Source: https://www.gnu.org/software/bash/manual/html_node/Command-Grouping

Groups commands to be executed in the current shell environment, avoiding subshell creation. Variable assignments persist after execution. Requires a semicolon or newline after the command list and whitespace separation for the braces.

```bash
{ list; }
```

--------------------------------

### Execute Commands in Subshell with Parentheses () in Bash

Source: https://www.gnu.org/software/bash/manual/html_node/Command-Grouping

Groups commands to be executed within a new subshell environment. Variable assignments made within the subshell do not persist after its completion. Redirections applied to this group affect all commands within it.

```bash
( list )
```

--------------------------------

### Bash printf Date Formatting with %(datefmt)T

Source: https://www.gnu.org/software/bash/manual/html_node/Bash-Builtins

The `%(datefmt)T` format specifier in Bash's `printf` command allows for custom date-time string formatting using `strftime(3)`. It accepts seconds since the epoch as an argument, with special values for current time (-1) and shell invocation time (-2).

```bash
printf '%(%Y-%m-%d %H:%M:%S)T\n' -1
```

--------------------------------

### Execute Command on Non-Zero Exit Status with trap ERR

Source: https://www.gnu.org/software/bash/manual/html_node/Bourne-Shell-Builtins

The `trap ERR` command executes an action whenever a pipeline, list, or compound command returns a non-zero exit status. There are specific conditions under which this trap is not executed, related to loops, conditionals, pipelines, and negation.

```bash
trap 'action' ERR
```

--------------------------------

### Duplicate File Descriptors in Bash

Source: https://www.gnu.org/software/bash/manual/html_node/Redirections

Duplicates an input or output file descriptor. `[n]<&word` copies an input descriptor, and `[n]>&word` copies an output descriptor. If `word` is `-`, the descriptor is closed. If `n` is omitted, standard input or output is used.

```bash
[n]<&word
```

```bash
[n]>&word
```

--------------------------------

### Bash Programmable Completion: Add Suffix to Completions (-S)

Source: https://www.gnu.org/software/bash/manual/html_node/Programmable-Completion-Builtins

Appends a specified suffix to each possible completion after all other options have been applied. This can be used to automatically add file extensions or other trailing characters.

```bash
# Example usage:
# compspec -S ".log"
```

--------------------------------

### Bash Parameter Length Expansion

Source: https://www.gnu.org/software/bash/manual/html_node/Shell-Parameter-Expansion

Substitutes the length in characters of the value of `parameter`. If `parameter` is '*' or '@', it substitutes the number of positional parameters. If `parameter` is an array name subscripted by '*' or '@', it substitutes the number of elements in the array. Negative indices count back from the end of the array.

```bash
${#parameter}
```

--------------------------------

### Compound Assignment for Associative Array in Bash

Source: https://www.gnu.org/software/bash/manual/html_node/Arrays

Assigns key-value pairs to an associative array. Each pair consists of a key followed by its corresponding value. The subscript (key) is required for each assignment.

```bash
my_assoc_array=([key1]=value1 [key2]=value2)
```

--------------------------------

### Bash: Prevent Overwriting Files with set -C

Source: https://www.gnu.org/software/bash/manual/html_node/The-Set-Builtin

The `set -C` option in Bash prevents output redirection operators like '>', '>&', and '<>' from overwriting existing files. To force overwriting, the '>|' operator must be used. This option enhances safety by preventing accidental data loss.

```bash
# Enable noclobber mode
set -C

# Create a file (will fail if it exists)
echo "Initial content" > existing_file.txt

# Attempt to overwrite (will fail)
echo "New content" > existing_file.txt

# Force overwrite using '>|'
echo "Overwritten content" >| existing_file.txt

# Disable noclobber mode
set +C
```

--------------------------------

### Bash: Convert Case with Pattern Matching

Source: https://www.gnu.org/software/bash/manual/html_node/Shell-Parameter-Expansion

These expansions modify the case of alphabetic characters in a parameter based on a pattern. The '^' and ',' operators affect the first character, while '^^' and ',,' affect all matching characters. If the pattern is omitted, it matches every character.

```Bash
`${parameter^pattern}`
`${parameter^^pattern}`
`${parameter,pattern}`
`${parameter,,pattern}`
```

--------------------------------

### Echo Text with Special Character Interpretation in Bash

Source: https://www.gnu.org/software/bash/manual/html_node/Bash-Builtins

The 'echo' command outputs its arguments, separated by spaces and terminated by a newline. It supports interpreting backslash-escaped characters for special formatting like alerts, backspaces, newlines, and more. The -e option enables this interpretation, while -E disables it.

```bash
echo "Hello\nWorld"
echo -e "\a\b\t\r\v\"\\"
echo -E "This will not interpret \n"
```

--------------------------------

### Bash: Enable Restricted Shell Mode with set -r

Source: https://www.gnu.org/software/bash/manual/html_node/The-Set-Builtin

The `set -r` option enables restricted shell mode in Bash, limiting certain operations to enhance security. This mode cannot be unset once enabled. It's primarily used for creating a safer environment for users with limited privileges.

```bash
# Enable restricted shell mode
set -r

# Attempting to change directory (may be restricted)
cd /tmp

# Attempting to change shell options (likely to fail in restricted mode)
set +x
```

--------------------------------

### Bash Arithmetic Expansion ((...))

Source: https://www.gnu.org/software/bash/manual/html_node/Conditional-Constructs

The `(( expression ))` construct in Bash evaluates an arithmetic expression. It returns a status of 0 if the expression evaluates to non-zero, and 1 otherwise. This is commonly used for numerical comparisons and calculations within scripts.

```bash
(( expression ))

```

--------------------------------

### Bash Builtin: Colon (:) Command

Source: https://www.gnu.org/software/bash/manual/html_node/Bourne-Shell-Builtins

The colon builtin command in Bash performs argument expansion and redirections without executing any other commands. It always returns a zero exit status.

```bash
: [arguments]
```

--------------------------------

### Exit the shell with a status code

Source: https://www.gnu.org/software/bash/manual/html_node/Bourne-Shell-Builtins

The `exit` command terminates the current shell process and returns a specified exit status to the parent process. If no status is provided, it defaults to the status of the last executed command. Any `EXIT` traps are executed before termination.

```bash
exit [n]
```

--------------------------------

### Move File Descriptors in Bash

Source: https://www.gnu.org/software/bash/manual/html_node/Redirections

Moves a file descriptor to another descriptor. `[n]<&digit-` moves an input descriptor, and `[n]>&digit-` moves an output descriptor. The original descriptor (`digit`) is closed after being duplicated.

```bash
[n]<&digit-
```

```bash
[n]>&digit-
```

--------------------------------

### Expand All Elements of Indexed Array in Bash

Source: https://www.gnu.org/software/bash/manual/html_node/Arrays

Expands to all elements of an indexed array as separate words. When enclosed in double quotes, '${name[@]}' expands each element into a distinct word, preserving spaces within elements.

```bash
echo "${my_array[@]}"
```

--------------------------------

### Bash: Replace Pattern at End

Source: https://www.gnu.org/software/bash/manual/html_node/Shell-Parameter-Expansion

Replaces the pattern if it matches at the end of the parameter's expanded value. The replacement string undergoes various expansions.

```bash
${parameter/%pattern/string}
```

--------------------------------

### Bash Variable Name Expansion

Source: https://www.gnu.org/software/bash/manual/html_node/Shell-Parameter-Expansion

Expands to the names of variables whose names begin with a specified prefix. When '@' is used within double quotes, each variable name expands to a separate word. The separator is the first character of the `IFS` variable.

```bash
${!prefix*}
${!prefix@}
```

--------------------------------

### Bash Array Index Expansion

Source: https://www.gnu.org/software/bash/manual/html_node/Shell-Parameter-Expansion

If `name` is an array variable, this expands to the list of array indices (keys) assigned in `name`. If `name` is not an array, it expands to 0 if `name` is set, and is null otherwise. When '@' is used within double quotes, each key expands to a separate word.

```bash
${!name[@]}
${!name[*]}
```

--------------------------------

### Bash fc Command: History Manipulation

Source: https://www.gnu.org/software/bash/manual/html_node/Bash-History-Builtins

The 'fc' command in Bash allows manipulation of the command history list. It can be used to edit and re-execute previous commands, or to list commands within a specified range. It supports string or numeric arguments for specifying command ranges and has options for editing, listing, and reversing the order.

```bash
fc [-e ename] [-lnr] [first] [last]
fc -s [pat=rep] [command]
```

--------------------------------

### Declare Associative Array in Bash

Source: https://www.gnu.org/software/bash/manual/html_node/Arrays

Explicitly declares a variable as an associative array using the 'declare -A' builtin command. This is necessary for creating arrays that use arbitrary strings as keys.

```bash
declare -A my_assoc_array
```

--------------------------------

### Bash Shopt Option: array_expand_once

Source: https://www.gnu.org/software/bash/manual/html_node/The-Shopt-Builtin

When set, 'array_expand_once' suppresses multiple evaluations of array subscripts during arithmetic evaluation and variable assignments. This option is related to 'assoc_expand_once'.

```bash
# If set, the shell suppresses multiple evaluation of associative and indexed array subscripts during arithmetic expression evaluation, while executing builtins that can perform variable assignments, and while executing builtins that perform array dereferencing.
```

--------------------------------

### Bash: Remove Shortest Prefix Pattern

Source: https://www.gnu.org/software/bash/manual/html_node/Shell-Parameter-Expansion

Removes the shortest matching pattern from the beginning of a parameter's expanded value. If the parameter is '@' or '*', it applies to all positional parameters or array members.

```bash
${parameter%word}
```

--------------------------------

### Bash String Substring Expansion

Source: https://www.gnu.org/software/bash/manual/html_node/Shell-Parameter-Expansion

Extracts a substring from a string variable using offset and optional length. Negative offsets count from the end. If length is omitted, it extracts to the end. If length is 0, it returns an empty string.

```bash
$ string=01234567890abcdefgh
$ echo ${string:7}
7890abcdefgh
$ echo ${string:7:0}

$ echo ${string:7:2}
78
$ echo ${string:7:-2}
7890abcdef
$ echo ${string: -7}
bcdefgh
$ echo ${string: -7:0}

$ echo ${string: -7:2}
bc
$ echo ${string: -7:-2}
bcdef
```

--------------------------------

### Expand All Elements of Indexed Array as Single Word in Bash

Source: https://www.gnu.org/software/bash/manual/html_node/Arrays

Expands to all elements of an indexed array as a single word, with elements separated by the first character of the IFS variable. When enclosed in double quotes, '${name[*]}' joins all elements into one string.

```bash
echo "${my_array[*]}"
```

--------------------------------

### Bash Function with Local Variable Shadowing

Source: https://www.gnu.org/software/bash/manual/html_node/Shell-Functions

Demonstrates how a local variable declared within a function shadows a global variable of the same name. References and assignments within the function scope affect only the local variable, leaving the global variable unmodified until the function returns.

```bash
func1()
{
    local var='func1 local'
    func2
}

func2()
{
    echo "In func2, var = $var"
}

var=global
func1

```

--------------------------------

### Compound Assignment with Subscripts for Indexed Array in Bash

Source: https://www.gnu.org/software/bash/manual/html_node/Arrays

Assigns values to specific indices within an indexed array using compound assignment. This allows for non-contiguous or out-of-order assignments.

```bash
my_array=([0]=value1 [2]=value3 [1]=value2)
```

--------------------------------

### Reference Associative Array Element in Bash

Source: https://www.gnu.org/software/bash/manual/html_node/Arrays

Retrieves the value associated with a specific key from an associative array. The key is provided as the subscript within the braces.

```bash
echo "${my_assoc_array[key1]}"
```

--------------------------------

### Bash Conditional Expression [[...]]

Source: https://www.gnu.org/software/bash/manual/html_node/Conditional-Constructs

The `[[ expression ]]` construct in Bash provides an enhanced conditional expression evaluation. It supports more advanced pattern matching and logical operations compared to the traditional `[` or `test` commands, offering greater flexibility in script logic.

```bash
[[ expression ]]

```

--------------------------------

### Bash Parameter Prefix Removal

Source: https://www.gnu.org/software/bash/manual/html_node/Shell-Parameter-Expansion

Removes the shortest matching `word` from the beginning of the value of `parameter`. If `word` begins with '#', the longest matching `word` is removed instead.

```bash
${parameter#word}
${parameter##word}
```

--------------------------------

### Declare Indexed Array in Bash

Source: https://www.gnu.org/software/bash/manual/html_node/Arrays

Explicitly declares a variable as an indexed array using the 'declare -a' builtin command. This ensures the variable will be treated as an indexed array, even before any elements are assigned.

```bash
declare -a my_array
```

--------------------------------

### Bash printf String and Character Formatting Modifiers

Source: https://www.gnu.org/software/bash/manual/html_node/Bash-Builtins

Bash's `printf` supports modifiers like 'l' for wide-character strings (%ls, %lc) and special handling for %b, %q, and %T specifiers that use field width and precision. Arguments are treated as C constants, with support for quoted characters.

```bash
printf '%-10.10s\n' "hello world"
```

```bash
printf '%q\n' "a string with spaces"
```

--------------------------------

### Detect Interactive Shell using '$-' in Bash

Source: https://www.gnu.org/software/bash/manual/html_node/Is-this-Shell-Interactive_003f

This snippet demonstrates how to check the special parameter '$-' to determine if the Bash shell is interactive. The parameter contains 'i' when the shell is interactive. This method is suitable for use in shell scripts.

```bash
case "$-" in
*i*)	echo This shell is interactive ;;
*)	echo This shell is not interactive ;;
esac

```

--------------------------------

### Remove Variables or Functions: unset

Source: https://www.gnu.org/software/bash/manual/html_node/Bourne-Shell-Builtins

The `unset` command removes shell variables or functions. Options `-v`, `-f`, and `-n` specify whether to remove a variable, a function, or a nameref, respectively. Readonly variables and functions cannot be unset.

```bash
unset [-fnv] [name]
```

--------------------------------

### Detect Interactive Shell using PS1 in Bash

Source: https://www.gnu.org/software/bash/manual/html_node/Is-this-Shell-Interactive_003f

This snippet shows how to check the environment variable PS1 to determine if the Bash shell is interactive. PS1 is unset in non-interactive shells and set in interactive shells. This is an alternative method for shell scripts.

```bash
if [ -z "$PS1" ]; then
        echo This shell is not interactive
else
        echo This shell is interactive
fi

```

--------------------------------

### Reference Indexed Array Element in Bash

Source: https://www.gnu.org/software/bash/manual/html_node/Arrays

Retrieves the value of a specific element from an indexed array using its numerical subscript. Braces are required around the array name and subscript to prevent conflicts with shell expansions.

```bash
echo "${my_array[0]}"
```

--------------------------------

### Set Readonly Variables and Functions in Bash

Source: https://www.gnu.org/software/bash/manual/html_node/Bourne-Shell-Builtins

The `readonly` command marks shell variables or functions as read-only, preventing their values from being changed. Options -a, -A, and -f specify if the name refers to an indexed array, associative array, or function, respectively. The -p option displays read-only attributes in a reusable format.

```bash
readonly [-aAf] [-p] [name[=value]] ...
```

--------------------------------

### Shift Positional Parameters in Bash

Source: https://www.gnu.org/software/bash/manual/html_node/Bourne-Shell-Builtins

The `shift` command modifies positional parameters by shifting them to the left. By default, it shifts by one (`n=1`), discarding `$1` and renaming subsequent parameters. If `n` is provided, it shifts by `n` positions. Parameters beyond the new `$#` are unset.

```bash
shift [n]
```

--------------------------------

### Remove Directories from Stack (Bash)

Source: https://www.gnu.org/software/bash/manual/html_node/Directory-Stack-Builtins

The `popd` command removes elements from the directory stack. Without arguments, it removes the top directory and changes to the new top directory. Options allow for suppressing directory changes or removing specific entries by index.

```bash
popd [-n] [+N | -N]
```

--------------------------------

### Bash: Remove Shortest Suffix Pattern

Source: https://www.gnu.org/software/bash/manual/html_node/Shell-Parameter-Expansion

Removes the shortest matching pattern from the end of a parameter's expanded value. If the parameter is '@' or '*', it applies to all positional parameters or array members.

```bash
${parameter#word}
```

--------------------------------

### Assign Value to Indexed Array Element in Bash

Source: https://www.gnu.org/software/bash/manual/html_node/Arrays

Assigns a value to a specific element of an indexed array. The subscript must be a non-negative integer. If the array is not yet declared, this syntax will implicitly create it as an indexed array.

```bash
my_array[0]=value1
my_array[1]=value2
```

--------------------------------

### Reference Last Element of Indexed Array in Bash

Source: https://www.gnu.org/software/bash/manual/html_node/Arrays

References the last element of an indexed array using a negative index. An index of -1 refers to the last element, -2 to the second to last, and so on, counting back from the end.

```bash
echo "${my_array[-1]}"
```

--------------------------------

### Bash unalias Command to Remove Aliases

Source: https://www.gnu.org/software/bash/manual/html_node/Bash-Builtins

The 'unalias' command removes aliases defined in the Bash shell. It can remove specific named aliases or all aliases if the -a option is provided. The command returns true if successful, and false if a specified alias is not found.

```bash
unalias [-a] [name ... ]
```

--------------------------------

### Bash: Remove Longest Prefix Pattern

Source: https://www.gnu.org/software/bash/manual/html_node/Shell-Parameter-Expansion

Removes the longest matching pattern from the beginning of a parameter's expanded value. If the parameter is '@' or '*', it applies to all positional parameters or array members.

```bash
${parameter%%word}
```

--------------------------------

### Append to Indexed Array in Bash

Source: https://www.gnu.org/software/bash/manual/html_node/Arrays

Appends a new value to the end of an indexed array using the '+=' operator with compound assignment syntax. This is a convenient way to add elements without explicitly managing indices.

```bash
my_array+=("new_value")
```

--------------------------------

### Bash: Remove Longest Suffix Pattern

Source: https://www.gnu.org/software/bash/manual/html_node/Shell-Parameter-Expansion

Removes the longest matching pattern from the end of a parameter's expanded value. If the parameter is '@' or '*', it applies to all positional parameters or array members.

```bash
${parameter##word}
```

=== COMPLETE CONTENT === This response contains all available snippets from this library. No additional content exists. Do not make further requests.