# Django installation for Python3+
**Step 1:** Install ``pip3``
To install pip3 on Ubuntu, Debian or Linux Mint:
```shell
sudo apt-get install python-pip3
```
To install pip3 on Fedora:
```shell
sudo yum install python-pip3
```
**Step 2:** Get the latest official version
```shell
pip3 install Django
```
Or  you can type the double equal sign and the version mark to install it explicitly.
```shell
pip3 insall Django==2.0.5
```
**Step 3:** Verifying
```shell
python3 -c "import django; print(django.get_version())"
```
