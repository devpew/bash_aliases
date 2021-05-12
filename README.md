# bash_aliases

### fav
```sh
alias mv="mv -iv"
alias cp="cp -riv"
alias mkdir="mkdir -vp"
```

### clear
```sh
alias c='clear'
```

### passwordstore for insert new passrord
```sh
alias p='pass insert -m'
```

### extended ls
```sh
alias ll='ls -la'
```

### ls with hidden files
```sh
alias l.='ls -d .* --color=auto'
```

### fast back cd
```sh
alias ..='cd ..'
alias ...='cd ../../../'
alias ....='cd ../../../../'
alias .....='cd ../../../../'
alias .4='cd ../../../../'
alias .5='cd ../../../../..'
```

### history
```sh
alias h='history'
```

### show pathes
```sh
alias path='echo -e ${PATH//:/\\n}'
```

### ping 5 sec
```sh
alias ping='ping -c 5'
```

### wakeup on lan (replace macs on yours)
```sh
alias wakeupnas01='/usr/bin/wakeonlan 00:11:32:11:15:FC'
alias wakeupnas02='/usr/bin/wakeonlan 00:11:32:11:15:FD'
alias wakeupnas03='/usr/bin/wakeonlan 00:11:32:11:15:FE'
```

### update for Debian-like distro
```sh
alias updatey="sudo apt-get --yes"
alias update='sudo apt-get update && sudo apt-get upgrade'
```

### nginx reload 
```sh
alias nginxreload='sudo /usr/local/nginx/sbin/nginx -s reload'
```

### backup scripts
```sh
alias backup='sudo /home/scripts/admin/scripts/backup/wrapper.backup.sh --type local --taget /raid1/backups'
alias nasbackup='sudo /home/scripts/admin/scripts/backup/wrapper.backup.sh --type nas --target nas01'
alias s3backup='sudo /home/scripts/admin/scripts/backup/wrapper.backup.sh --type nas --target nas01 --auth /home/scripts/admin/.authdata/amazon.keys'
alias rsnapshothourly='sudo /home/scripts/admin/scripts/backup/wrapper.rsnapshot.sh --type remote --target nas03 --auth /home/scripts/admin/.authdata/ssh.keys --config /home/scripts/admin/scripts/backup/config/adsl.conf'
alias rsnapshotdaily='sudo  /home/scripts/admin/scripts/backup/wrapper.rsnapshot.sh --type remote --target nas03 --auth /home/scripts/admin/.authdata/ssh.keys  --config /home/scripts/admin/scripts/backup/config/adsl.conf'
alias rsnapshotweekly='sudo /home/scripts/admin/scripts/backup/wrapper.rsnapshot.sh --type remote --target nas03 --auth /home/scripts/admin/.authdata/ssh.keys  --config /home/scripts/admin/scripts/backup/config/adsl.conf'
alias rsnapshotmonthly='sudo /home/scripts/admin/scripts/backup/wrapper.rsnapshot.sh --type remote --target nas03 --auth /home/scripts/admin/.authdata/ssh.keys  --config /home/scripts/admin/scripts/backup/config/adsl.conf'
```

### linux memory
```sh
alias meminfo='free -m -l -t'
```

### show top process eating RAM
```sh
alias psmem='ps auxf | sort -nr -k 4'
alias psmem10='ps auxf | sort -nr -k 4 | head -10'
```

### show top process eating CPU
```sh
alias pscpu='ps auxf | sort -nr -k 3'
alias pscpu10='ps auxf | sort -nr -k 3 | head -10'
```

### GPG
```sh
alias gpg-secret='gpg -K '
alias gpg-public='gpg -k '
alias gpg-new='gpg --full-gen-key && echo "keyid-format 0xlong"'
alias gpg-encrypt='gpg -e -a -r '
alias gpg-decrypt='gpg -d -o '
alias gpg-export-public='gpg --export -a '
alias gpg-export-secret='gpg --export-secret-key -a '
```

### Git
```sh
alias gs='git status'
alias ga='git add'
alias ga.='git add .'
alias gch='git checkout'
alias gchb='git checkout -b'
alias gc='git commit'
alias gcm='git commit -m'
alias gb='git branch'
alias mergemaster='git checkout master; git pull; git merge develop; git push; git checkout develop'
alias gfr='git fetch upstream && git rebase upstream/master'
```
### GIT add, commit, push
```sh
function acp() {
git add .
git commit -m "$1"
git push
}
```


### NPM
```sh
alias s='npm start'
```

### Docker
```sh
#alias di='docker images'
#alias dr='docker run'
#alias db='docker build' 
#alias dp='docker ps'
alias dps="docker ps -a"
alias di="docker images"
alias drmi="docker rmi"
alias drm="docker rm"
```

### Get last Docker container id
```sh
alias d:last="docker ps -lq"
```

### Open a bash terminal in last Container if arguments are different than 1
### Open a bash terminal in the container passed through argument 1 (id or name)
```sh
d:bash () {
  if [ $# != 1 ]; then
    docker exec -it `d:last` bash
  else
    docker exec -it $1 bash
  fi
}
```


### With no argument runs a bash terminal in a new ubuntu container(could be specified any image) with current directory content mapped to '/app' inside container. If an image is passed to the first argument this one will run. If multiples arguments append to the image.
```sh
d:run () {
  if [ $# == 0 ]; then
    docker run -it -v `pwd`:/app -w /app --rm buildpack-deps:trusty bash
  elif [ $# == 1 ]; then
    docker run -it -v `pwd`:/app -w /app --rm $1 
  else
    docker run -it -v `pwd`:/app -w /app --rm $1 ${@:2}
  fi
}
```

### kuber
```sh
alias k="kubectl"
alias ka="kubectl apply -f"
alias kpa="kubectl patch -f"
alias ked="kubectl edit"
alias ksc="kubectl scale"
alias kex="kubectl exec -i -t"
alias kg="kubectl get"
alias kga="kubectl get all"
alias kgall="kubectl get all --all-namespaces"
alias kinfo="kubectl cluster-info"
alias kdesc="kubectl describe"
alias ktp="kubectl top"
alias klo="kubectl logs -f"
alias kn="kubectl get nodes"
alias kpv="kubectl get pv"
alias kpvc="kubectl get pvc"
```

### Golang
```sh
alias gog='go get'
alias gor='go run'
alias gob='go build'
```

### My IP
```sh
function myip()
{
    extIp=$(dig +short myip.opendns.com @resolver1.opendns.com)

    printf "Wireless IP: "
    MY_IP=$(/sbin/ifconfig wlp4s0 | awk '/inet/ { print $2 } ' |
      sed -e s/addr://)
    echo ${MY_IP:-"Not connected"}


    printf "Wired IP: "
    MY_IP=$(/sbin/ifconfig enp0s25 | awk '/inet/ { print $2 } ' |
      sed -e s/addr://)
    echo ${MY_IP:-"Not connected"}

    echo ""
    echo "WAN IP: $extIp"

}
```

### REPEAT
```sh
function repeat()      
{
    local i max
    max=$1; shift;
    for ((i=1; i <= max ; i++)); do  # --> C-like syntax
        eval "$@";
    done
}
```

### Show/hide hidden files in the macOS Finder
```sh
alias show="defaults write com.apple.finder AppleShowAllFiles -bool true && killall Finder"
alias hide="defaults write com.apple.finder AppleShowAllFiles -bool false && killall Finder"
```

### This Ubuntu default is great for sending notifications when a long running command exits:
```sh
alias alert='notify-send --urgency=low -i "$([ $? = 0 ] && echo terminal || echo error)" "$(history|tail -n1|sed -e '\''s/^\s*[0-9]\+\s*//;s/[;&|]\s*alert$//'\'')"'
```

### Brew update
```sh
alias brewupdate='brew update && brew upgrade --all && brew cask update && brew cleanup && brew cask cleanup'
```

### MAC OS Recursively delete those annoying .DS_Store files.
```sh
alias cleanup="find . -type f -name '*.DS_Store' -ls -delete"
```

### Extract the contents of a .tar file.
```sh
alias untar='tar -xvf'
```

### Print out the local IP on en0.
```sh
alias iplocal='ifconfig en0 | grep --word-regexp inet | awk "{print $2}"'
```

### Print out the public ip address.
```sh
alias ippub="dig +short myip.opendns.com @resolver1.opendns.com"
```

### Generate a random 20 character password using OpenSSL.
```sh
alias randpass="openssl rand -base64 20"
```

### extract anything
```sh
extract () {
  if [ -f $1 ] ; then
    case $1 in
      *.tar.bz2)  tar xjf $1    ;;
      *.tar.gz) tar xzf $1    ;;
      *.bz2)    bunzip2 $1    ;;
      *.rar)    rar x $1    ;;
      *.gz)   gunzip $1   ;;
      *.tar)    tar xf $1   ;;
      *.tbz2)   tar xjf $1    ;;
      *.tgz)    tar xzf $1    ;;
      *.zip)    unzip $1    ;;
      *.Z)    uncompress $1 ;;
      *)      echo "'$1' cannot be extracted via extract()" ;;
    esac
  else
    echo "'$1' is not a valid file"
  fi
}
```

### Send my Mac to sleep:
```sh
alias sleep="pmset sleep now"
```

### I'M LOVING IT
```sh
alias fuck='sudo !!'
```

### MAC OS Change directory to the current Finder directory
```sh
function cdf() {
    target=`osascript -e 'tell application "Finder" to if (count of Finder windows) > 0 then get POSIX path of (target of front Finder window as text)'`
    if [ "$target" != "" ]; then
        cd "$target"; pwd
    else
        echo 'No Finder window found' >&2
    fi
}
```

### Run make from a sub-directory of a project.
```sh
mk (){
        if [ $PWD == "/" ]; then
                echo "FAILED :("
        elif [ ! -f Makefile ]; then
                pushd .. > /dev/null
                mk $*
                popd > /dev/null
        else 
                pwd
                echo make $*
                make $*
        fi
}
```



