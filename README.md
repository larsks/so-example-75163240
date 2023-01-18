This repository accompanies my answer to <https://stackoverflow.com/q/75163240/147356>.

To run this example:

```
ansible-playbook playbook.yaml
```

Expected output:

```
PLAY [all] *********************************************************************

TASK [Get Instance Inventory] **************************************************
changed: [node0]
changed: [node1]
changed: [node2]

PLAY [localhost] ***************************************************************

TASK [create merged inventory] *************************************************
ok: [localhost] => (item=node0)
ok: [localhost] => (item=node1)
ok: [localhost] => (item=node2)

TASK [show merged inventory] ***************************************************
ok: [localhost] => {
    "inventory_data": "hostname: node0\r\nhostname: node1\r\nhostname: node2\r\n"
}

TASK [send to api] *************************************************************
ok: [localhost]

TASK [verify post data] ********************************************************
ok: [localhost] => {
    "post_result.content|from_json": {
        "args": {},
        "data": "",
        "files": {},
        "form": {
            "hostname: node0\r\nhostname: node1\r\nhostname: node2\r\n": ""
        },
        "headers": {
            "Accept-Encoding": "identity",
            "Content-Length": "51",
            "Content-Type": "application/x-www-form-urlencoded",
            "Host": "httpbin.org",
            "User-Agent": "ansible-httpget",
            "X-Amzn-Trace-Id": "Root=1-63c84ac5-2b1b31f71363406f055e4b6f"
        },
        "json": null,
        "origin": "172.59.152.250",
        "url": "https://httpbin.org/post"
    }
}

PLAY RECAP *********************************************************************
localhost                  : ok=4    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
node0                      : ok=1    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
node1                      : ok=1    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
node2                      : ok=1    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   

```
