**DevOps with Docker**

Exercices from https://devopswithdocker.com/part1/

Part 1

Ex 1.1



**Ex 1.7**

Dockerfile:
```
FROM ubuntu:16.04

WORKDIR /mydir
RUN apt-get update && apt-get install -y curl


COPY myscript.sh .
RUN chmod +x myscript.sh
CMD ["sh", "myscript.sh"]
```

myscript.sh:
```
echo "Input website:"; read website; echo "Searching.."; sleep 1; curl http://$website;
```

Commands:
```
docker build -t curler
docker run -it curler
```

Output:
```
Input website:
helsinki.fi
Searching..
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>301 Moved Permanently</title>
</head><body>
<h1>Moved Permanently</h1>
<p>The document has moved <a href="http://www.helsinki.fi/">here</a>.</p>
</body></html>
```



**Ex 1.8**

```
docker run --mount source=testvol1,target=/usr/app devopsdockeruh/first_volume_exercise
```

cd to /var/lib/docker/volumes/testvol1/_data

```
[root@hostname _data]# cat logs.txt
Sun, 19 Jul 2020 19:07:25 GMT
Sun, 19 Jul 2020 19:07:28 GMT
Sun, 19 Jul 2020 19:07:31 GMT
Sun, 19 Jul 2020 19:07:34 GMT
Secret message is:
"Volume bind mount is easy"
```


**Ex 1.9**

```
docker run -d -p 5555:80 devopsdockeruh/ports_exercise
```

Browse to http://localhost:5555

```
Ports configured correctly!!
```
