# 1 TypeError: unsupported operand type(s) for -=: 'Retry' and 'int'
```
Collecting setuptools
Exception:
Traceback (most recent call last):
File "/usr/lib/python2.7/dist-packages/pip/basecommand.py", line 209, in main
status = self.run(options, args)
File "/usr/lib/python2.7/dist-packages/pip/commands/install.py", line 328, in run
wb.build(autobuilding=True)
File "/usr/lib/python2.7/dist-packages/pip/wheel.py", line 748, in build
self.requirement_set.prepare_files(self.finder)
File "/usr/lib/python2.7/dist-packages/pip/req/req_set.py", line 360, in prepare_files
ignore_dependencies=self.ignore_dependencies))
File "/usr/lib/python2.7/dist-packages/pip/req/req_set.py", line 577, in _prepare_file
session=self.session, hashes=hashes)
File "/usr/lib/python2.7/dist-packages/pip/download.py", line 810, in unpack_url
hashes=hashes
File "/usr/lib/python2.7/dist-packages/pip/download.py", line 649, in unpack_http_url
hashes)
File "/usr/lib/python2.7/dist-packages/pip/download.py", line 842, in _download_http_url
stream=True,
File "/usr/share/python-wheels/requests-2.9.1-py2.py3-none-any.whl/requests/sessions.py", line 480, in get
return self.request('GET', url, **kwargs)
File "/usr/lib/python2.7/dist-packages/pip/download.py", line 378, in request
return super(PipSession, self).request(method, url, *args, **kwargs)
File "/usr/share/python-wheels/requests-2.9.1-py2.py3-none-any.whl/requests/sessions.py", line 468, in request
resp = self.send(prep, **send_kwargs)
File "/usr/share/python-wheels/requests-2.9.1-py2.py3-none-any.whl/requests/sessions.py", line 576, in send
r = adapter.send(request, **kwargs)
File "/usr/share/python-wheels/CacheControl-0.11.5-py2.py3-none-any.whl/cachecontrol/adapter.py", line 46, in send
resp = super(CacheControlAdapter, self).send(request, **kw)
File "/usr/share/python-wheels/requests-2.9.1-py2.py3-none-any.whl/requests/adapters.py", line 376, in send
timeout=timeout
File "/usr/share/python-wheels/urllib3-1.13.1-py2.py3-none-any.whl/urllib3/connectionpool.py", line 610, in urlopen
_stacktrace=sys.exc_info()[2])
File "/usr/share/python-wheels/urllib3-1.13.1-py2.py3-none-any.whl/urllib3/util/retry.py", line 228, in increment
total -= 1
TypeError: unsupported operand type(s) for -=: 'Retry' and 'int'
```
solution1:
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py  \
python get-pip.py \

solution2:
sudo python -m pip install --upgrade --force pip

solution3:
sudo pip install ipython==8888 #先指定一个不存在的版本以查看可用版本，发现5版本中有5.5.0（你的可能不一样）
sudo pip install ipython==5.5.0

# 2 执行sudo apt-get install python-pip 出现错误：E: Unable to locate package python-pip
python-pip is in the universe repositories, therefore use the steps below:
```
sudo apt-get install software-properties-common
sudo apt-add-repository universe
sudo apt-get update
sudo apt-get install python-pip
```



