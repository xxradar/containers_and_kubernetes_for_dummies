```
$ sudo crictl list

$ sudo crictl inspect e6120476c6999 | jq -r .info.pid
5333

$ sudo ps -ax -o pid,netns,cmd | grep -i 5333
 5333 4026532876 node ./index.js

$ sudo ps -ax -o pid,netns,cmd | grep -i 4026532876
 4870 4026532876 /pause
 5333 4026532876 node ./index.js
$
````
