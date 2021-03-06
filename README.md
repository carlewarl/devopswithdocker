**DevOps with Docker**

Exercices from https://devopswithdocker.com/part1/

Part 1


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


**Ex 1.10**

dockerfile

```
FROM ubuntu:latest

WORKDIR /usr/app
RUN apt update && apt upgrade -y
RUN apt install -y curl
RUN apt install -y npm
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash
RUN apt install -y nodejs
COPY frontend-example-docker/ .
RUN npm config set strict-ssl false
RUN npm install

RUN npm install -g serve

EXPOSE 5000

CMD ["serve", "-s", "-l", "5000", "dist"]
```

Commands:

```
docker build -t ex110 .
docker run -it -p 5000:5000 ex110
```

**Ex 1.11**

dockerfile

```
FROM ubuntu:latest

WORKDIR /usr/app
RUN apt update && apt upgrade -y
RUN apt install -y curl
RUN apt install -y npm
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash
RUN apt install -y nodejs
COPY backend-example-docker/ .
RUN npm config set strict-ssl false
RUN npm install

RUN npm install -g serve

EXPOSE 8000

CMD ["server", "-s", "-l", "5000", "dist"]
```

Commands:

```
docker build -t ex111 .
docker run --mount source=ex111vol,target=/usr/app -p 8000:8000 ex111
```

**Ex 1.12**

