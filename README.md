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
