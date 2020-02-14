# Non-exhaustive list of steps to set up a new computer

# SSH
## on old computer:
cp -r ~/.ssh ~/Desktop/ssh
## AIRDROP TO NEW COMPUTER
## on new comp:
cp ~/Downloads/ssh/* ~/.ssh
ssh-add -K

# System Preferences
  - Keyboard
    - Set keyboard repeat to max speed
    - Set keyboard delay to min wait
    - Use function keys as function keys (need to Hold "Fn" to get "special" functions
    - Set Spotlight shortcut to option - space (use command - space for Quicksilver)
    - Shorcuts -> click on "Use keyboard navigation to move focus..."
  - Trackpad
    - Tap to click on trackpad
  - General
    - Show Scroll Bars (always)
 
# Install
## IT installed R/3.4 and Rstudio - which asked for command line tools, which installed
## waiting on sudo/admin access!

## R (say 'N' if an offer of compiliation comes up)
  - R/3.6 and Rstudio 1.2 (latest)
  - `install.packages(c('Seurat', 'tidyverse', 'pals','ggforce','ggrepel','devtools',  'cowplot','sctransform','plotly','httr','igraph','leiden','lmtest','metap','uwot','RccpEigen'))`

## brew
  - https://brew.sh
  - https://gist.github.com/irazasyed/7732946
