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

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/154b5fcc-07bb-447a-a5f5-20c4f38fd5d1/a9db368e-23f6-4e7a-8d90-ac2ba8f5c9fa/Untitled.png)

/etc/suricata

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/154b5fcc-07bb-447a-a5f5-20c4f38fd5d1/1398f622-dd3c-4c16-a782-457f6f35e4e1/Untitled.png)

`/var/log/suricata`

`cat fast.log`

→ 로그를 확인해보면 gilgil.net, netflix.com(막힘, UDP), qt.io(잡히긴 하는데 로그 하나 뜨고 막힘 TCP → UDP)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/154b5fcc-07bb-447a-a5f5-20c4f38fd5d1/6b825f82-7fcc-495e-a8aa-cfd2f9759793/Untitled.png)
