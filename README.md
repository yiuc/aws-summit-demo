# aws-summit-demo

Class: AWS
Created: May 19, 2023 2:40 PM
Reviewed: No

- [open a cloud9 to develop your code](https://docs.aws.amazon.com/corretto/latest/corretto-17-ug/amazon-linux-install.html)
[https://tinyurl.com/2tjze7vv](https://tinyurl.com/2tjze7vv)

```bash
# Java 17
# Your favorite IDE
# Git, or Git support in your IDE

sudo yum install java-17-amazon-corretto-devel
sudo alternatives --config java
```

- install [git-remote-codecommit](https://pypi.org/project/git-remote-codecommit/) using python

```
pip install git-remote-codecommit
```

- Clone the webgoat https://github.com/WebGoat/WebGoat to local
[https://tinyurl.com/57fa8atd](https://tinyurl.com/57fa8atd)

```
git clone https://github.com/WebGoat/WebGoat.git
git checkout v2023.4
```

- create codecommit repo

```
aws codecommit create-repository --repository-name aws-summit --repository-description "Test web goat" --tags Team=aws
```

- config remote repo

```
git remote add codecommit codecommit::ap-southeast-1://aws-summit
```

- push repo to codecommit

```
git push codecommit
```

- [Create a CodeCommit repository association (CodeGuru Reviewer console)](https://docs.aws.amazon.com/codeguru/latest/reviewer-ug/create-codecommit-association.html)

[https://tinyurl.com/yc2k42eu](https://tinyurl.com/yc2k42eu)

Running webgoat

```bash
./mvnw clean install
docker build -f Dockerfile . -t webgoat/webgoat
```

```bash
# run java
./mvnw spring-boot:run
# run docker
docker run --name webgoat -it -p 127.0.0.1:8080:8080 -p 127.0.0.1:9090:9090 webgoat/webgoat
```

```bash
curl http://localhost:8080/WebGoat
```
