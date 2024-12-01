## Local Port Forwarding

Windows --> Parrot ssh no directamente expuesto.
bash```
```
parrot: python3 -m http.server 8080
Windows: ssh -L 9090:localhost:8080 kmxbay@192.168.32.128
Windows: http://localhost:9090
```

## Remote Port Forwarding


```
Windows: ssh -R 9090:localhost:8000 kmxbay@192.168.32.128
```

## Dynamic Port Forwarding

Con proxy SOCKS navegar desde Windows
```
ssh -D 1080 kmxbay@192.168.32.128
```

