DevOps with Docker

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

