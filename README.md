# suricata

`sudo apt install suricata` → suricata 설치

`/etc/suricata`에 rules 만들기

`etc/suricata/rules` 에 test.rules 만들기

`touch test.rules`

`vim test.rules`

alert tcp any any -> any 80 (msg:"[gilgil.net](http://gilgil.net/) access"; content:"GET /"; content:"Host: "; content:"[gilgil.net](http://gilgil.net/)"; sid:10001; rev:1;)
alert tcp any any -> any 80 (msg:"[netflix.com](http://netflix.com/) access"; content:"GET /"; content:"Host: "; content:"[netflix.com](http://netflix.com/)"; sid:10002; rev:1;)
alert tcp any any -> any 80 (msg:"[qt.io](http://qt.io/) access"; content:"GET /"; content:"Host: "; content:"[qt.io](http://qt.io/)"; sid:10003; rev:1;)

터미널 2개 띄워놓고 브라우저 [gilgil.net](http://gilgil.net) 띄워놓기

터미널 1개에 `suricata -s test.rules -i eth0` 실행

터미널 1개에는 `tail -f /var/log/suricata/fast.log`

아까 test.rules에 추가했던 게 [gilgil.net](http://gilgil.net/) , [netflix.com](http://netflix.com/), [qt.io](http://qt.io/) 이기 때문에 브라우저에서 링크 열기

/etc/suricata


`/var/log/suricata`

`cat fast.log`

→ 로그를 확인해보면 gilgil.net, netflix.com(막힘, UDP), qt.io(잡히긴 하는데 로그 하나 뜨고 막힘 TCP → UDP)
