Autoscp
=======

A helper script to automatically upload local files to a remote location when they are changed locally.

Basic Usage:
------------

    $ python autoscp --help
    
    usage: autoscp [-h] [-c] [--host HOST] [--root ROOT] [--identity-file I]
               folders [folders ...]

    Automatic Remtoe SCP On Local File Change

    positional arguments:
        folders            The folders to upload to remote host

    optional arguments:
        -h, --help         show this help message and exit
        -c, --create       Upload Everything On Start
        --host HOST        The remote host to SCP to
        --root ROOT        The remote root directory to SCP to
        --identity-file I  The absolute path to your pem key

You can specify your default values within the scipt itself, or override these with the command line arguments:

    REMOTE_HOST_DEFAULT  = 'user@xxx.xxx.xxx.xxx'
    REMOTE_ROOT_DEFAULT  = '/path/to/remote/dir'
    ABSOULTE_PEM_DEFAULT = '/path/to/your/local/pemfile'

Usage:
    
    $ python autoscp --host=ubuntu@some_ec2_public_dns --root=/home/ubuntu/ /home/fin/my_dir/ 

Include List:
-------------

Append regex strings into this array to include files.

    includes = ['*'] # Edit this to include files: Note: for files only

Exclude List:
-------------

Append regex strings into this array to exclude files or folders.

    excludes = ['*/.git', '*.pyc'] # Exclude List for dirs and files

Notes:
------

Relative paths are currently not handled well within the autoscp script (work in progress) so use absolute paths.

For Example:

    $ python autoscp ./this_dir/ 

Will not work correctly, paths specified by ~ *should* work however this hasn't been tested yet.

Secondly, SCP will not recursively create directories, so if you create a file within a new sub-directory which does not currently exist remotely the upload will fail. Specifying the -c flag will circumnavigate this at the minor cost of a one of ssh mkdir command.