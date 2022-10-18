How to start Jupyter notebook on remote server (ex. _Calchas_)

1. Αρχικό **ssh** στον server.
	`$ ssh -p 15000 kmexis@calchas.gr`

2. Start Jupyter:
	`$ jupyter notebook --no-browser --port=<PORT>`

3. Run on local machine:
	`$ ssh -p 15000 -L <PORT>:localhost:<PORT> kmexis@calchas.imsi.athenarc.gr`

4. Open browser on local machine:
	`url: localhost:<PORT>`

- List active Internet connections: `$ sudo netstat -plten`
- Kill process (if PORT is used already by another jupyter): `$ kill -9 <PID>`
 
**TIP**: Start `Jupyter` as root: `$ sudo -i`


