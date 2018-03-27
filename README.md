# spring-boot-docker-simple

This is just a simple example and details about how to build a web service using spring boot and docker.

Originally based on [this](https://spring.io/guides/gs/spring-boot-docker/) example.

## Spring Boot
* very simple hello world application 
* Several ways to run this: 
    * From IDEA, open the Application class and click Run or Debug on the class itself - Spring Boot Magic ensues!
    * mvn clean install from the command line.  Then, java -jar target/gs-spring-boot-docker-0.1.0.jar
    * Run it from Docker!  (see below)
* http://localhost:8080/


## Docker
* see pom file (docker-maven-plugin)
* see Dockerfile
    * The Dockerfile is very simple - just Java 8 and Alpine and our app
* mvn install docker:build to build the docker image and install it.  You can also run the docker plugin from the IDEA mvn projects window which I find easier.
* docker images to see your image
* Run it: docker run -p 8080:8080 -t springio/gs-spring-boot-docker
* docker ps to see it running, hit URL
* Can also run with: ./runDocker
* Be sure to kill it when done
    * docker ps, or docker container ls
    * docker stop <containerId>
* Debugging
    * All works great - just debug as remote with the port and you are golden assuming the ports are mapped when running docker (see runDocker.sh)
* PUSHING
    * This is installed locally, but we need to push a docker image in order to run it from somewhere else (like EC2)

## Docker in AWS
* create EC2 instance - see Amazon docs, just login anf hit create
* ssh -i "dev/keys/tom-test-server.pem" ec2-user@ec2-34-217-126-99.us-west-2.compute.amazonaws.com
* install docker, etc.   https://docs.aws.amazon.com/AmazonECS/latest/developerguide/docker-basics.html#install_docker
* Pushing this to AWS so that it can be run in EC2 was a bit of a chore, but doable.
    * Essentially, you must setup amazon container repository, then (from your local machine that has the image), login to that repository, and then push the image to it.  Once this is done, you can go to the EC2 and docker run teh image.
        * docker login -u AWS -p eyJwYXlsb2FkIjoiSjFINkNDM2Jrb0VmT2U2Qzd6OUd6bzlya1JLak5KMzNXYk5xUUFtNkNha2lDMW9yQXBLSERmTFNpZW03eDU5Zy9FQzVORkxTRGFJU0Y3TWJlV3pJM3MyalpMeUNoaHprNXRVWnM4YUt2TmhCVm1EYWpVMCtBcXFuMDB0VkdpaVByZHZGZGt0djU3VnpUUHZ0eUp2TU1RbURRZFBtOUFKN0F2NS8rbnYxbmZHRHFuRTNpY0dRWXNXVHc3RXVqU1RFcHhIQWdEOWREa2Q1cy9iYlQxM3pBUlAwdDh4TkhmQ2h3QVh6REQza0I1akx0Mm1CRENkU3BSTmZtbU41bDhMd1NQdi9WUHRNN3h0SXk1dGZ1SXBWVVJJejVJdzFUazNuLy9OelA5aWlldU4zZ09Tc1ZZOXRNNkpaaUJ6aXIxc1RaYWNiOFJycFo1Qmx4VXYzeUZsUHM3MzVvWGVjeEVrblpNckhlb2ZUdXExVWNSRlFFSTdSVVU2RmVlbklBQVBhenZ6aGpFS3NzOGI4cXdDTFh3MHQ1VFpUaE1nNXJxMDY3OFRHT3p6UnBIcVZlUXZpbHBhRm1WTXdjVFFsWXRhVnRkdHBGV1Y3MGZhTzlySTNwL3p4R3RteVdxVHlYVW96emtRQ0F5aldSSmVKNzQ0dVRHY1YyL0hVS2NhWFg5VnVMclFEZ21wVVBVVTg3T0M0Z2VqVC91MFZUelVPZWdJQUt0UVJic2dYMHhqVUU2R0RjelZlOUx1Tjc4UnVoMnN4Nkc3K0l6bUJTMzBDZ1hZWHdaejJWblZBVWRmTVQyVjl3RWRqZ0JoWXFzcHUzU1FtaDFsbjh0WnQ5Uyt4WmZoc3JhT2NWR0I2UE5oVmQ0RGRLNVgxNkJSSWZ0VzBUQUpka1FTaHNjS0Fkc054VkZxWUxtRVBtbk1veEc2WnZDOUdrWW05d2lCay9WYlVwelBYMXIvTi9kanYxdXhyYWtJSmsyZThoSDFvdXY1eDN1TkdwdXUvVWV5K2Q1eVBMd0xuVmxGN1JPYXRXeUY1YVQyZGdZdDlwRW41N01NbjY5ZlBSYlhyTFVHZGwxTTdBRWNBNEU2aW91Ykw2Z1ZpOU1oK25FWW9mTHJNWlQ3bGhyUGQ3Vk5NbnR0cUVsTkRoMVQzMnF4b2lzRkxKKzJBNGpkY3FXNDJkREs2aHdHWVRxUDVyVGFGWUpLRS9EYVdpMzF1QlZ2bGZGUU5seVFZdjJibDdZS0ptQVI2TTdnUlpTQ1VtSVo1dWNXaHlKbmxLS2ZaSWVEL0Zwa3ZpdjJ2a3Y2VDB6OUFPVkw0ZWRqWitvblRuYjVHSWdIVDRranVET3YwRjE4L1hlQnN0M3lpODFIdTYrTzB2dnpHK2x3aXN2V1JabUF4ZzEvR2NsMlUraENacGtPZ3FCUXFoT1dubUJwWUtRMmJxSXVqZExRQVhvb2VHZEdqYUxRUW5jR1BLY2Q5dHQ4QUtsWVBadmFydFBiajIyS1NOYkhNIiwiZGF0YWtleSI6IkFRRUJBSGo2bGM0WElKdy83bG4wSGMwMERNZWs2R0V4SENiWTRSSXBUTUNJNThJblV3QUFBSDR3ZkFZSktvWklodmNOQVFjR29HOHdiUUlCQURCb0Jna3Foa2lHOXcwQkJ3RXdIZ1lKWUlaSUFXVURCQUV1TUJFRURGT1FhdG5EaGtWdDZ6VDJSZ0lCRUlBN3hON3RabjcyMUxLb29uVjZndmtVRkE4Skd4VG9mdDBFUXVNdDBxcTl5VTllQUR4VXBzVm1kbGxNc1dqQnhoNDdEOVM2V1I0UVlwTkFFeWM9IiwidmVyc2lvbiI6IjIiLCJ0eXBlIjoiREFUQV9LRVkiLCJleHBpcmF0aW9uIjoxNTIyMTY1Mzg3fQ== https://312113887026.dkr.ecr.us-west-2.amazonaws.com
        * docker tag springio/gs-spring-boot-docker:latest 312113887026.dkr.ecr.us-west-2.amazonaws.com/toms-docker-repo:latest
        * docker push 312113887026.dkr.ecr.us-west-2.amazonaws.com/toms-docker-repo:latest          



## Notes



