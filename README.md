# The verification of the ansible module

I have copied the ansible's copy module's source code copy.py to the project's root directory as c_copy.py("c_copy" module),
and execute the task used the "c_copy" module.
As a result, I can't understand but the task have failed although the task used the "copy" module have suceeeded.

## Requirements

* Python 2.7.12(pyenv)
* pip
* Vagrant

## Setup

```
$ git clone https://github.com/suzuki-shunsuke/ansible-module-test-example
$ cd ansible-module-test-example
$ pyenv install 2.7.12
$ pip install --upgrade pip
$ pip install --upgrade virtualenv
$ virtualenv env
$ source env/bin/activate
$ cp env/lib/python2.7/site-packages/ansible/modules/core/files/copy.py c_copy.py
```

## Test

```
$ vagrant up --provision-with=ansible
```

## tasks/main.yml

```yaml
- name: run the copy module
  copy:
    src: test.txt
    dest: /tmp/test.txt
- name: run the clone of the copy module
  c_copy:
    src: test.txt
    dest: /tmp/c_test.txt
```

## Result

```
TASK [copy : run the copy module] **********************************************
changed: [default]

TASK [copy : run the clone of the copy module] *********************************
fatal: [default]: FAILED! => {"changed": false, "failed": true, "msg": "Source test.txt not found"}
```
