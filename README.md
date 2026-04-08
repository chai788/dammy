# dammy
<dependencies>
        <!-- JUnit -->
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter</artifactId>
            <version>5.9.3</version>
            <scope>test</scope>
        </dependency>
    </dependencies>

//
    public void testAdd() {
        Addition add1 = new Addition();
        int expectedResult = 10;
        int actualResult = add1.add(5, 2);
        assertEquals(expectedResult, actualResult);
    }

   // dockerfile
   FROM python:3.9-slim
WORKDIR /app
COPY app.py .
RUN pip install flask
EXPOSE 5020
CMD ["python", "app.py"]

// app.py 
from flask import Flask

app = Flask(__name__)

@app.route("/")
def home():
    return "Hello from Docker!"

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)




Experiment 15: Introduction to Docker and Basic Commands 
Tasks: Install Docker, run sample containers. 
Outcome: Container fundamentals. 
1st start docker desktop
docker ps
docker ps -a
docker images
docker run hello-world
docker pull nginx
docker run -d -p 8000:80 nginx
docker ps
docker stop <con id>
docker rm <con id>
docker ps


Experiment 16: Creating Docker Images using Dockerfile 
Tasks: Write Dockerfile, build and run image. 
Outcome: Application containerization. 

create 3 files
sample.py
app.py
Dockerfile
-> docker build -t my-python-app .
-> docker images
-> docker run -p 5000:5000 my-python-app
-> then see localhost:5000


Experiment 17: Docker Volumes and Port Mapping 
Tasks: Map ports and volumes. 
Outcome: Data persistence knowledge.

1st start docker desktop
docker run -d nginx
docker images
(=> localhost:8000 => to see nginx web page)
docker volume create myvolume
docker volume create dvolume
docker volume ls
docker run -it -v myvolume:/data ubuntu bash
-> then write below code
cd data

echo "docker volume persisted Test" > test.txt
exit

again run

docker run -it -v myvolume:/data ubuntu bash

cd data
cat /data/test.txt
exit

Experiment 18: Docker Image Push to Docker Hub 
Tasks: Push Docker image to Docker Hub. 
Outcome: Image distribution understanding.

create files in one folder
stream dockerfile
app.py
=> open cmd
docker ps
docker build -t java-app .
docker run -d -t java-app
docker ps
docker build -t chainapatil/java-app:v1 .
docker run -d -t chainapatil/java-app:v1
docker logout
docker login
-> username & password
docker push chainapatil/java-app:v1
docker tag java-app chainapatil/java-app:v1
