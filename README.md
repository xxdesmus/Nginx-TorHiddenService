###$ This is a simple docker-compose script to host a website powered by nginx on a Tor hidden service.

Build status: [![Circle CI](https://circleci.com/gh/xxdesmus/Nginx-TorHiddenService.svg?style=svg)](https://circleci.com/gh/xxdesmus/Nginx-TorHiddenService)

Assumptions:
1. You have docker installed and running.
2. You have docker-compose installed.

1. ```git clone git@github.com:xxdesmus/Nginx-TorHiddenService.git```
2. ```cd nginx/html```
3. edit index.html however you'd like to
4. ```docker build -t PickNameHere/nginx_alpine .```
5. Test that nginx is working with your webpage -> ```docker run -d --name nginx -p 80:80 PickNameHere/nginx_alpine```
6. ```docker ps``` -> get the container ID -> ```docker stop container ID```
7. ```cd ..```
8. ```docker-compose up -d```
9. ```docker-compose ps``` -> confirm both nginx and tor are running
10. ```docker-compose logs tor``` -> look for ```Your onion address is XXXXXXXX.onion```
11. Wait roughly 2-3 minutes for the hidden service to become active, then go to ```XXXXXXXX.onion``` in the Tor browser.
12. Profit. You just published a website on a Tor hidden service.
