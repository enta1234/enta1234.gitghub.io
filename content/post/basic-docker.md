---
title: "Basic Docker"
date: 2019-03-10T23:02:09+07:00
draft: true
---

# [basic_docker] | เจ้า docker ปลาตัวน้อย
  >docker เป็น software container ทำงานได้รวดเร็ว ลดขั้นตอนการติดตั้ง os ลง โดยเปลี่ยนเป็น **image file** ให้เรียกใช้ได้ง่ายขึ้น เมื่อสั่งให้ images ทำงาน จะเปลี่ยนสถานะเป็น **container** และสามารถติดตั้ง application server ก็สามารถทำได้ง่ายเพราะ docker มีลักษณะเป็น **infrastructure-as-code** (image >> container)

## basic command
command | comment | ex.
--------|----------|---------
docker [options] command| syntex ในการเรียกใช้คำสั่ง docker | `docker -v` or `docker docker build .`
docker images [options] | แสดง images ที่มีอยู่ในเครื่อง | `docker images` or `docker images -a`
docker ps [options] | แสดง container ที่มีอยู่ในเครื่อง | `docker ps` or `docker ps -a`
docker pull <images_name> | download images จาก repositories | `docker pull alpine` or `docker pull mongo`
docker run [options] <images_id/images_name> | เรียกใช้งาน images ให้ทำงานขึ้นมาเป็น container | `docker run -dit --name entro01 alpine` or `docker run -dit -p 3000:80 -v /myapp:/app/ --name app01 alpine`
docker exec -it <container_id/container_name> [scripting] | จะทำการ execute เข้าไปใน container โดยการใช้ script ซึ่งส่วนมากจะมี sh กับ bash | `docker exec -it entro01 sh`
docker start <container_id/container_name> | เริ่มใช้งานของ container ที่ stop อยู่ | `docker start entro01` or `docker start 440as5ddaa66`
docker stop <container_id/container_name> | หยุดการทำงานของ container ที่ start อยู่ | `docker stop entro01` or `docker stop 440as5ddaa66`
docker rm [options] <container_id/container_name> | ทำการลบ container ที่ระบุ ด้วย id หรือ name | `docker rm entro01` or `docker rm -f 440as5ddaa66`
docker rmi [options] <images_id/images_name> | ทำการลบ images ที่ระบุ ด้วย id | `docker rmi entro01` or `docker rmi -f 440as5ddaa66`

## cp1 pull images
  >ให้ทำการ pull **image** ลงมาไว้ภายในเครื่อง

  `>_ docker pull alpine`
  `>_ docker pull python:2.7.16-alpine3.8`

## cp2 run container
  >ทำการใช้งาน image ที่ได้ pull ลงมา โดยเปลี่ยนเป็น **container** ด้วยคำสั่ง run
 
  - 1 `>_ docker run --rm -it --name entro01 alpine`
  - 2 `>_ docker run -dit -p 3000:3000 --name entro01 alpine`
  - 3 `>_ docker run --rm -it -w /app/myweb --expose 3000 -p 3000:3000 --mount .\:/app/myweb python:2.7.16-alpine3.8 python main.py`
  
## cp3 Dockerfile
  >เราสามารถคำสั่งของ docker เก็บไว้เป็นไฟล์ได้เราจะเรียกไฟล์นั้นว่า Dockerfile
  
  `>_ cd your/project`
  
  `>_ vi Dockerfile`
  
  ตัวอย่าง [Dockerfile](https://github.com/enta1234/basic_docker/blob/master/Dockerfile).
  
## cp4 build image
  >เมื่อเตรียม Dockerfile เสร็จเราสามารถ image ของเราเองได้

  `>_ docker build -t myweb:1.0.0 .`

  >หรือในกรณีที่เราไมได้ตั้งชื่อไฟล์ว่า Dockerfile ให้เราระบุให้ชัดเจน

  `>_ docker build -t myweb:1.0.0 ./docker-file`

  ex.

  `>_ docker run -dit -p 8000:8000 --name webEntro myweb:1.0.0`

## cp5 stop-start-delete
  ex. stop container

  `>_ docker stop webEntro`

  ex. start container

  `>_ docker stop webEntro`

  ex. delete container

  `>_ docker rm -f webEntro`

  ex. delete images

  `>_ docker rmi -f myweb:1.0.0`

  ex. delete, stop and start all container.

  `>_ docker rm -f $(docker ps -qa)`

  ex. delete all images.

  `>_ docker rmi -f $(docker images -q -a)`

  (อ่านเพิ่มเติมได้ที่)[https://github.com/enta1234/docker-cp]