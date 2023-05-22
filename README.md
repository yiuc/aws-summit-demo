# aws-summit-2023-demo

## 1. Provison Devlopment environment in Cloud9 (optional)

- open a cloud9 to develop your code

[install Java 17](https://docs.aws.amazon.com/corretto/latest/corretto-17-ug/amazon-linux-install.html)

```bash
# Java 17
# Your favorite IDE
# Git, or Git support in your IDE

sudo yum install java-17-amazon-corretto-devel
sudo alternatives --config java
```

## 2. Setup repository 
- install [git-remote-codecommit](https://pypi.org/project/git-remote-codecommit/) using python

```
pip install git-remote-codecommit
```

- create codecommit repo

```
aws codecommit create-repository --repository-name aws-summit --repository-description "Test web goat" --tags Team=aws
```

- Clone the webgoat https://github.com/WebGoat/WebGoat to local

```
git clone https://github.com/WebGoat/WebGoat.git
git checkout v2023.4 # released version
```

- config remote repo

```
git remote add codecommit codecommit::ap-southeast-1://aws-summit
```

- push repo to codecommit

```
git push codecommit
```

## 3. Associate your repository and run the CodeGuru analysis

[Create a CodeCommit repository association (CodeGuru Reviewer console)](https://docs.aws.amazon.com/codeguru/latest/reviewer-ug/create-codecommit-association.html)

## 4. Compile webgoat source code

```bash
./mvnw clean install
docker build -f Dockerfile . -t webgoat/webgoat
```

## 5. Running webgoat

```bash
# run by java
./mvnw spring-boot:run
# run by docker
docker run --name webgoat -it -p 127.0.0.1:8080:8080 -p 127.0.0.1:9090:9090 webgoat/webgoat
```

## 6. Quick testing command

```bash
curl -L http://localhost:8080/WebGoat
```
