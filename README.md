# Cowrie
(Antisyphon training lab from Cyber Deception/Active Defense)
## Running Cowrie
- Become root (```sudo su -```) and use Docker to deploy Cowrie:
<pre>docker run -p 2222:2222 cowrie/cowrie</pre>
 <img width="800" alt="Screenshot 2025-03-31 at 2 34 12 PM" src="https://github.com/user-attachments/assets/61f10ff0-67e0-4668-94cf-baa91e2b4436" />  <br><br>
- In another terminal window, run this command to remove the ```known_hosts``` file from the .ssh directory.
<pre>rm .ssh/known_hosts</pre>
- Connect to the honeypot with this command:
<pre>ssh -p 2222 root@localhost</pre>
<img width="800" alt="Screenshot 2025-03-31 at 2 36 35 PM" src="https://github.com/user-attachments/assets/f26c4c6f-a475-422f-99b0-a38ec2ae0182" /><br><br>
- Type ```yes``` to continue connecting and ```12345``` for the password
- Run a few commands:
<pre>whoami
id
pwd</pre>
- They will appear in the logs:<br><br>
<img width="800" alt="Screenshot 2025-03-31 at 2 40 27 PM" src="https://github.com/user-attachments/assets/af3699e1-fcd2-48d7-860c-357e844ba2e0" /><br><br>
<img width="800" alt="Screenshot 2025-03-31 at 2 44 46 PM" src="https://github.com/user-attachments/assets/88979c07-537e-420b-b461-aadde381d3e4" /><br><br>

- Let's stop this session (```ctrl+c``` in the logs terminal) and attempt to enhance realism by changing the hostname and mimicking a real system banner:
- As root, run this command:
<pre>vim /var/lib/docker/overlay2/49cb1d1569dac74ee9793c9efb526ae1ba35b8e4a31b14a1a1c8c30bc70dc953/diff/cowrie/cowrie-git/etc/cowrie.cfg.dist</pre>
- To make changes, press ```a```. Then press, ```esc```, ```:```, ```wq!```, and ```return```
<img width="600" alt="Screenshot 2025-03-31 at 2 50 46 PM" src="https://github.com/user-attachments/assets/a68109dc-fb52-4a73-b471-a41866c3b278" /><br><br>
- Restart Cowrie:
<pre>docker run -p 2222:2222 cowrie/cowrie</pre>
- Remove known_hosts:
<pre>rm .ssh/known_hosts</pre>
- Connect again:
<pre>ssh -p 2222 root@localhost</pre>
- Type ```yes``` and ```12345```
- Hostname is changed:<br><br>
<img width="800" alt="Screenshot 2025-03-31 at 3 08 20 PM" src="https://github.com/user-attachments/assets/8a4d67a7-bd1a-464c-9f18-1930f9f3d0cb" /><br><br>

- Now for the message of the day banner:
<pre>vim /var/lib/docker/overlay2/49cb1d1569dac74ee9793c9efb526ae1ba35b8e4a31b14a1a1c8c30bc70dc953/diff/cowrie/cowrie-git/honeyfs/etc/motd</pre> 
- My MOTD:
<pre>
Welcome to the internal SSH server.

Unauthorized access is strictly prohibited.
All actions are logged and monitored.

Contact IT for support
</pre>
- Restart Cowrie again:
<pre>docker run -p 2222:2222 cowrie/cowrie</pre>
<pre>rm .ssh/known_hosts

ssh -p 2222 root@localhost</pre>
<img width="800" alt="Screenshot 2025-03-31 at 3 17 15 PM" src="https://github.com/user-attachments/assets/7f00c1d2-0eb7-4c40-a71f-09d7bee89d27" /><br><br>
- MOTD changed.
