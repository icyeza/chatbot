readme
AI Chatbot Application by Lorita
This project is a straightforward web application with a conversational interface for an AI chatbot. It is intended to illustrate load balancing, deployment, and web development strategies. You may find comprehensive instructions on how to execute the application locally, deploy it to web servers, and set up a load balancer to guarantee scalability and dependability below.
features a chatbot UI that is responsive.
Load-balanced deployment for high availability.
Technology utilized JavaScript, HTML, and CSS for the application.
Node.js is hosted using a web server.
HAProxy for load balancing
Clone the repository:

bash
Copy code
git clone  https://github.com/icyeza/chatbot.git
cd chatbot
Install http-server: npm install -g http-server
Start the application: http-server -p 5500 --host 0.0.0.0
Access the app at http://127.0.0.1:5500.

Deployment to Servers
Clone the repository on both Web01 and Web02 servers:
git clone https://github.com/icyeza/chatbot.git
cd chatbot
Start the server on each machine: http-server -p 5500 --host 0.0.0.0
Open port 5500:
sudo ufw allow 5500
Test each server using curl or a browser:
curl http://52.91.2.150:5500
curl http://34.229.144.175:5500
Configuring the Load Balancer
Edit /etc/haproxy/haproxy.cfg on the load balancer server:

haproxy
frontend www-https
    bind *:443
    default_backend app-backend

backend app-backend
    balance roundrobin
    server web01 52.91.2.150:5500 check
    server web02 34.229.144.175:5500 check
Restart HAProxy: sudo systemctl restart haproxy
Test the load balancer by accessing its IP: http://34.227.49.173

APIs Used
GOOGLE AI studio: Enables conversational capabilities.
Documentation: GOOGLE AI studio
Challenges and Solutions
Port 5500 Access: Resolved by allowing traffic through the firewall using ufw.
Load Balancer Misconfiguration: Fixed by ensuring correct server definitions and using roundrobin.
Credits
API: OpenAI API for chatbot functionalities.
Tools: http-server for hosting, HAProxy for load balancing.
Documentation:
GOOGLE AI Studio
HAProxy Official Docs
