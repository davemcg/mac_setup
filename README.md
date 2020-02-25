# Non-exhaustive list of steps to set up a new Mac (Catalina)
  
## Move over SSH keys
  - on old computer:
    - cp -r ~/.ssh ~/Desktop/ssh
  - `AirDrop` to new computer
  - on new comp:
    - cp ~/Downloads/ssh/* ~/.ssh
    - ssh-add -K

## NFS Link to Arges NAS
  - (no switch or intermediate network connection between the NAS and the desktop)
  - (on Arges), copy subnet and IP address, go into NFS share pref on Arges and make new IP address (use below on Mac)
  - (on Mac), System Preferences -> Network -> Ethernet -> Configure IPv4 "manually", set IP address, match subnet to Arges
  - `sudo mount -t nfs -o resvport,rw 10.1.1.ArgesAddress:/volume1/Arges /Volumes/Arges/`
  
## vim ~/.bash_profile
```
# mcgaughey stuffs
alias ls='ls -G'
alias ll='ls -ltrhcF'
HISTSIZE=100000000
HISTFILESIZE=10000000
shopt -s histappend
export PROMPT_COMMAND="history -a; history -c; history -r; $PROMPT_COMMAND"
export HISTTIMEFORMAT="%y/%m/%d %T "
```
then run `source ~/.bash_profile` to load for session

To get it to always load add `source ~/.bash_profile` to /etc/profile


## System Preferences
  - Keyboard
    - Set keyboard repeat to max speed
    - Set keyboard delay to min wait
    - Use function keys as function keys (need to Hold "Fn" to get "special" functions
    - Set Spotlight shortcut to option - space (use command - space for Quicksilver)
    - Shortcuts -> click on "Use keyboard navigation to move focus..."
  - Trackpad
    - Tap to click on trackpad
  - General
    - Show Scroll Bars (always)
 
## Install

  - XQuartz: https://www.xquartz.org
  - R (say 'N' if an offer of compiliation comes up)
    - R/3.6 and Rstudio 1.2 (latest)
      - Turn off workspace save in Rstudio
    - `install.packages(c('Seurat', 'tidyverse', 'pals','ggforce','ggrepel','devtools','blogdown',  'cowplot','sctransform','plotly','httr','igraph','leiden','lmtest','metap','uwot','RccpEigen'))`
    - `BiocManager::install(c('BiocGenerics', 'DelayedArray', 'DelayedMatrixStats', 'limma', 'S4Vectors', SingleCellExperiment', 'SummarizedExperiment', 'batchelor', 'scran', 'scater', 'batchelor'))`

  - brew
    - https://brew.sh
    - Install failed this worked -> https://gist.github.com/irazasyed/7732946
    - Afterwards, install `gcc` so you can compile packages for `R` (see below for instructions on how to get `R` to recognize `gcc`)
      - `brew install gcc`
    - `brew cask install keepingyouawake` # little menu bar GUI for caffeinate (prevent mac from sleeping)

  - SourceTree: https://www.sourcetreeapp.com
  
  - Quicksilver: https://qsapp.com
    - Enable clipboard for copy/paste history save (https://qsapp.com/manual/Clipboard%20and%20Shelf/)

  - iTerm
    - fix word jump: https://coderwall.com/p/h6yfda/use-and-to-jump-forwards-backwards-words-in-iterm-2-on-os-x
    
  - TextMate: https://macromates.com
  
## Get `R` to recognize your `gcc`

  - Install `R` and `gcc` as above (`brew` for `gcc`)
  - Create `~/.R/Makevars` and use the below
  - To find out which version of `gcc` you have check the `/usr/local/Cellar/gcc/`path and edit the top line `VER=-` and the bottom `FLIBS` line to match
    ```
    VER=-9
    CC=gcc$(VER)
    CXX=g++$(VER)
    CXX11=g++$(VER)
    CXX14=g++$(VER)
    CXX17=g++$(VER)
    CFLAGS=-mtune=native -g -O2 -Wall -pedantic -Wconversion
    CXXFLAGS=-mtune=native -g -O2 -Wall -pedantic -Wconversion
    FLIBS=-L/usr/local/Cellar/gcc/9.2.0_3/lib/gcc/9/
    ```
  
## NIH specific
  - Get "aa" account (email Michael Wright) to get admin/sudo permission
  - requires signatures from boss (Brian Brooks) and NEI SIO
  - Globus: https://hpc.nih.gov/storage/globus.html
