##OSX-Config

####Installation
To install simply:

1. Clone the repository into your development directory.
2. Run the `inst` install script:

    ./inst

####Default Configuration
By default the script will add some aliases and configure git with some basic color settings and adjust your bash prompt. You will want to update the settings in the `bashrc.part` file of the `git-configure` module to reflect your personal details. 

In addition it will:

* Replace your `.bash_profile` file.
* Assemble a `bashrc.build` file and then replace your `.bashrc` file with it.

####Custom Configuration
Because I don't want to publicize all of my system specific settings or aliases to private machines there is a `bashrc.part.local` file in the `default-configure` module that if present will append any settings in that file to the `bashrc.build` file on installation. This file is ignored by git and so won't be committed to the repository.

####Extending
Typically you would extend the file by customizing the `bashrc.part` files and then installing again. However in some situations you may want to add another module to compartmentalize specific settings. To do that you would:

1. Create a new module folder/
2. Create new `bashrc.part` and `inst` files in that folder.
3. Update these files to reflect your desired settings and any installation commands you would want to be run.

Here is an example of the `bashrc.part` file in the `git-configure` module:
    
    #!/bin/bash
    BASEDIR=$(dirname $0)
    mkdir -pv ~/osx-config/git/
    cp -rf $BASEDIR/lib/git-completion ~/osx-config/git/
    cp -rf $BASEDIR/lib/git-bash-completion ~/osx-config/git/
    git config --global user.name "Jason Fox"
    git config --global user.email jasonrobertfox@gmail.com
    git config --global color.branch auto
    git config --global color.diff auto
    git config --global color.status auto
    
    if [ ! -f $BASEDIR/../bashrc.build ]; then
    	$BASEDIR/../bashrc.build
    fi
    
    cat $BASEDIR/bashrc.part >> $BASEDIR/../bashrc.build 