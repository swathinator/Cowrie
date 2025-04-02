# Cowrie
(Antisyphon training lab from Cyber Deception/Active Defense)<br><br>
Full lab explanation available on my <a href="https://medium.com/@swathitadepalli/active-defense-and-cyber-deception-antisyphon-training-44c0ee851be4#aafe">Medium</a>
## Deploy Cowrie Using Docker
- Switch to the root user (```sudo su -```) and start the Cowrie container:
<pre>docker run -p 2222:2222 cowrie/cowrie</pre>
 <img width="800" alt="Screenshot 2025-03-31 at 2 34 12 PM" src="https://github.com/user-attachments/assets/61f10ff0-67e0-4668-94cf-baa91e2b4436" />  <br><br>
- In a new terminal window, remove the ```known_hosts``` file: 
<pre>rm .ssh/known_hosts</pre>
- Connect to the honeypot:
<pre>ssh -p 2222 root@localhost</pre>
<img width="800" alt="Screenshot 2025-03-31 at 2 36 35 PM" src="https://github.com/user-attachments/assets/f26c4c6f-a475-422f-99b0-a38ec2ae0182" /><br><br>
- Type ```yes``` to continue connecting and enter ```12345``` as the password.
- Run a few commands:
<pre>whoami
id
pwd</pre>
- These commands will be logged in Cowrie:<br><br>
<img width="800" alt="Screenshot 2025-03-31 at 2 40 27 PM" src="https://github.com/user-attachments/assets/af3699e1-fcd2-48d7-860c-357e844ba2e0" /><br><br>
<img width="800" alt="Screenshot 2025-03-31 at 2 44 46 PM" src="https://github.com/user-attachments/assets/88979c07-537e-420b-b461-aadde381d3e4" /><br><br>
## Change the hostname and MOTD
- Let's attempt to enhance realism by changing the hostname and mimicking a real system banner:
- Stop this session by pressing ```Ctrl + C``` in the logs terminal.
- As root, edit the Cowrie configuration file:
<pre>vim /var/lib/docker/overlay2/49cb1d1569dac74ee9793c9efb526ae1ba35b8e4a31b14a1a1c8c30bc70dc953/diff/cowrie/cowrie-git/etc/cowrie.cfg.dist</pre>
- In Vim, press ```a``` to enter edit mode, then press ```Esc```, type ```:wq!```, and hit ```Enter``` to save.
<img width="600" alt="Screenshot 2025-03-31 at 2 50 46 PM" src="https://github.com/user-attachments/assets/a68109dc-fb52-4a73-b471-a41866c3b278" /><br><br>
- Restart Cowrie:
<pre>docker run -p 2222:2222 cowrie/cowrie</pre>
- Remove known_hosts again:
<pre>rm .ssh/known_hosts</pre>
- Reconnect:
<pre>ssh -p 2222 root@localhost</pre>
- Type ```yes``` and ```12345```
- The hostname should now be changed:<br><br>
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
