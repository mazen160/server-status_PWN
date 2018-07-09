*server-status PWN*
=====================

### A script that monitors and extracts requested URLs and clients connected to the service by exploiting publicly accessible Apache server-status instances ###


## What is Apache server-status? ##
Apache server-status is an Apache monitoring instance, available by default at `http://example.com/server-status`. In normal cases, the server-status instance is not accessible by non-local origin IPs. However, due to misconfiguration, it can be publicly accessible. This leads anyone to view the great amount of data by server-status.

A part of "interesting/severe" data to long-term attackers and red-teamers is the exposure of clients' IP addresses and requested URLs on the Apache service, which an exposed Apache server-status provides. Also, Apache server-status output is viewed on the real-time.

## What type of data can be exposed? ##
* All requested URLs by all Hosts/VHosts on the Apache server.
	* This includes:
		* Hidden and obscure files and directories.
		* Session Tokens on GET REQUEST_URI (eg.. `https://example.com/?token=123`). If tokens are passed through GET HTTP method, it will be exposed, no matter what SSL encryption is used.
* All clients' IP addresses along with URLs the clients have requested.

## What do we need as attackers? ##
We need a script that constantly monitors the exposed Apache server-status, and extracts all new URLs, and save them for later testing.

Also, if we are performing an intelligence engagement, we would need all IPs that interacts with the Apache server that hosts our target website, along with requested URLs. Then we need to constantly monitor the service on the hour.


# Introducing *server-status PWN* #
server-status PWN constantly requests and parse Apache server-status page for any new event. Whenever a new URL is requested and a new client IP address is used, it will be logged and reported.

It outputs the data in a SQLITE3 database, and includes an option for saving unique URLs in a newline-delimited file.


## **Usage** ##
`python server-status_PWN.py --url 'http://example.com/server-status'`


## **Why I created this?** ##
* To prove the severity of having an exposed Apache server-status. 
* `PoC || GO` supporter.
* I needed an actual PoC exploit.

# **Requirements** #
* Python2 or Python3
* requests
* bs4


## **Example Output** ##
![server-status_PWN Example Output](https://raw.githubusercontent.com/mazen160/public/master/static/images/server-status_PWN-Demo.png)


# **Legal Disclaimer** #
This project is made for educational and ethical testing purposes only. Usage of server-status_PWN for attacking targets without prior mutual consent is illegal. It is the end user's responsibility to obey all applicable local, state and federal laws. Developers assume no liability and are not responsible for any misuse or damage caused by this program.


# **License** #
The project is licensed under MIT License.

## **Note** ##
There are custom Apache server-status that would require a user to change table index values. If you're encountering errors related to this issue, refer to https://github.com/mazen160/server-status_PWN/issues/2.

# **Author** #
*Mazin Ahmed*
* Website: [https://mazinahmed.net](https://mazinahmed.net)
* Email: *mazin AT mazinahmed DOT net*
* Twitter: [https://twitter.com/mazen160](https://twitter.com/mazen160)
* Linkedin: [http://linkedin.com/in/infosecmazinahmed](http://linkedin.com/in/infosecmazinahmed)

