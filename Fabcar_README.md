# Fabric Network, fabcar-backend, fabcar-fontend

< Fabcar Application >

< FabCar Client download (React JS) >
참조 사이트 : https://github.com/chhaileng/fabcar-client
npm install express body-parser --save (필요시)
npm install socket.io (필요시)

< Network Setup >
1 Network (Hyperledger Fabric v1.4.3)
$ git clone https://github.com/hyperledger/fabric-samples.git
$ cd fabcar
$ ./startFabric.sh

2 Enroll admin and register user
$ cd fabcar/apiserver
$ node enrollAdmin.js
$ node registerUser.js
$ node query.js    //test

3 REST Server Run
$ node app.js

4 Client Application (Reactjs)
4.1 Download & npm install
~/fabric-samples/fabcar$ git clone https://github.com/chhaileng/fabcar-client.git
$ cd fabcar-client
$ npm install
(npm install 에러시..package-lock.json 삭제 후 재시도)

$ npm start

< Client Application Source 수정 >
REST Server 연동시 파일 수정
- AddCar.js : axios.post(http://master:3000/cars => http://도메인 또는 IP:3000/cars)
- AllCars.js : axios.post(http://master:3000/cars => http://도메인 또는 IP:3000/cars)
- ChangeOwner.js : axios.post(http://master:3000/cars => http://도메인 또는 IP:3000/cars)

Package.json Port 지정
-  "start": "export PORT=8080 && react-scripts start",

< Clean Up >
cd /fabric-samples/first-network
./byfn.sh down
docker rm $(docker ps -aq)
docker rmi $(docker images dev-* -q)
docker network prune

< Docker 명령어 >

1 이미지 리스트 확인
$ docker images

2 이미지 삭제(ID)
$ docker rmi e1de74e67cc7

3 컨테이너 목록 확인
$ docker ps -a
or 
$ docker container ls -a

4 컨테이너 삭제 (ID)
$ docker rm d1202a706e75

< IP정보 >

내부 공인 IP 확인 : ifconfig | egrep "(^\\w|inet )"  또는  ifconfig | grep "inet "
외부 공인 IP 확인 : curl ifconfig.me

< 네트워크 포트 정보 >
netstat -tnlp

포트 확인 : netstat -tnlp | grep 8080
포트 kill : kill -9 16940(PID)
