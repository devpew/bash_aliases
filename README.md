# bash_aliases

### clear
```
alias c='clear'
```

### passwordstore for insert new passrord
```
alias p='pass insert -m'
```

### extended ls
```
ll='ls -la'
```

### ls with hidden files
```
alias l.='ls -d .* --color=auto'
```

### fast back cd
```
alias ..='cd ..'
alias ...='cd ../../../'
alias ....='cd ../../../../'
alias .....='cd ../../../../'
alias .4='cd ../../../../'
alias .5='cd ../../../../..'
```

### history
```
alias h='history'
```

### show pathes
```
alias path='echo -e ${PATH//:/\\n}'
```

### ping 5 sec
```
alias ping='ping -c 5'
```

### wakeup on lan (replace macs on yours)
```
alias wakeupnas01='/usr/bin/wakeonlan 00:11:32:11:15:FC'
alias wakeupnas02='/usr/bin/wakeonlan 00:11:32:11:15:FD'
alias wakeupnas03='/usr/bin/wakeonlan 00:11:32:11:15:FE'
```

### update for dedian-like distro
```
alias updatey="sudo apt-get --yes"
alias update='sudo apt-get update && sudo apt-get upgrade'
```

### nginx reload 
```
alias nginxreload='sudo /usr/local/nginx/sbin/nginx -s reload'
```

### backup scripts
```
alias backup='sudo /home/scripts/admin/scripts/backup/wrapper.backup.sh --type local --taget /raid1/backups'
alias nasbackup='sudo /home/scripts/admin/scripts/backup/wrapper.backup.sh --type nas --target nas01'
alias s3backup='sudo /home/scripts/admin/scripts/backup/wrapper.backup.sh --type nas --target nas01 --auth /home/scripts/admin/.authdata/amazon.keys'
alias rsnapshothourly='sudo /home/scripts/admin/scripts/backup/wrapper.rsnapshot.sh --type remote --target nas03 --auth /home/scripts/admin/.authdata/ssh.keys --config /home/scripts/admin/scripts/backup/config/adsl.conf'
alias rsnapshotdaily='sudo  /home/scripts/admin/scripts/backup/wrapper.rsnapshot.sh --type remote --target nas03 --auth /home/scripts/admin/.authdata/ssh.keys  --config /home/scripts/admin/scripts/backup/config/adsl.conf'
alias rsnapshotweekly='sudo /home/scripts/admin/scripts/backup/wrapper.rsnapshot.sh --type remote --target nas03 --auth /home/scripts/admin/.authdata/ssh.keys  --config /home/scripts/admin/scripts/backup/config/adsl.conf'
alias rsnapshotmonthly='sudo /home/scripts/admin/scripts/backup/wrapper.rsnapshot.sh --type remote --target nas03 --auth /home/scripts/admin/.authdata/ssh.keys  --config /home/scripts/admin/scripts/backup/config/adsl.conf'
```

### linux memory
```
alias meminfo='free -m -l -t'
```

### show top process eating RAM
```
alias psmem='ps auxf | sort -nr -k 4'
alias psmem10='ps auxf | sort -nr -k 4 | head -10'
```

### show top process eating CPU
```
alias pscpu='ps auxf | sort -nr -k 3'
alias pscpu10='ps auxf | sort -nr -k 3 | head -10'
```

### GPG
```
alias gpg-secret='gpg -K '
alias gpg-public='gpg -k '
alias gpg-new='gpg --full-gen-key && echo "keyid-format 0xlong
alias gpg-encrypt='gpg -e -a -r '
alias gpg-decrypt='gpg -d -o '
alias gpg-export-public='gpg --export -a '
alias gpg-export-secret='gpg --export-secret-key -a '
```

### Git
```
#alias gs='git status'
#alias ga='git add'
#alias ga.='git add .'
#alias gch='git checkout'
#alias gchb='git checkout -b'
#alias gc='git commit'
#alias gcm='git commit -m'
#alias gb='git branch'
```

### Docker
```
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
```
alias d:last="docker ps -lq"
```

### Open a bash terminal in last Container if arguments are different than 1
### Open a bash terminal in the container passed through argument 1 (id or name)
```
d:bash () {
  if [ $# != 1 ]; then
    docker exec -it `d:last` bash
  else
    docker exec -it $1 bash
  fi
}
```


### With no argument runs a bash terminal in a new ubuntu container(could be specified 
### any image) with current directory content mapped to '/app' inside container.
### if an image is passed to the first argument this one will run.
### if multiples arguments append to the image.
```
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
```
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
```
#alias gog='go get'
#alias gor='go run'
#alias gob='go build'
```

### My IP
```
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
```
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
```
alias show="defaults write com.apple.finder AppleShowAllFiles -bool true && killall Finder"
alias hide="defaults write com.apple.finder AppleShowAllFiles -bool false && killall Finder"
```

### This Ubuntu default is great for sending notifications when a long running command exits:
```
alias alert='notify-send --urgency=low -i "$([ $? = 0 ] && echo terminal || echo error)" "$(history|tail -n1|sed -e '\''s/^\s*[0-9]\+\s*//;s/[;&|]\s*alert$//'\'')"'
```
