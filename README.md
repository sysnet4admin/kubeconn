# conn
Connect containter in a pod as bounce shell.

## Usage for Multi-Container 

### select namespace
```sh
[root@m-k8s]# kubectl conn

1 default
2 istio-system
3 kube-node-lease
4 kube-public
5 kube-system
6 single

Please select namespace <Press Enter to 'default'>:
```

### select pod  
```sh
1 details-v1-66b6955995-jkzh6
2 mutil-6b6cb6b558-67s5t
3 mutil-6b6cb6b558-mv4fz
4 mutil-6b6cb6b558-vjj9l
5 productpage-v1-5d9b4c9849-4v6x7
6 ratings-v1-fd78f799f-86b7j
7 reviews-v1-6549ddccc5-5hl9f
8 reviews-v2-76c4865449-j2cjf
9 reviews-v3-6b554c875-8wl4x

Please select pod in <default>: 2
1  istio-init
2  nginx
3  istio-proxy
```

### select container 
```sh
Please select container in <mutil-6b6cb6b558-67s5t>: 2
# bash
root@mutil-6b6cb6b558-67s5t:/#

```

### other container 
```sh
<snipped>
Please select pod in <default>: 2
1  istio-init
2  nginx
3  istio-proxy

Please select container in <mutil-6b6cb6b558-67s5t>: 3
$ bash
istio-proxy@mutil-6b6cb6b558-67s5t:/$
```

## Usage for Single-Container 
```sh
[root@m-k8s]# kubectl conn

1 default
2 istio-system
3 kube-node-lease
4 kube-public
5 kube-system
6 single

Please select namespace <Press Enter to 'default'>: 6
1 nginx-f89759699-5lqtx
2 nginx-f89759699-5qvvx
3 nginx-f89759699-8v9pm

Please select pod in <single>: 1
# bash
root@nginx-f89759699-5lqtx:/#
```


## Default bounce shell but bash can run if pod support it 
```sh
# bash
root@nginx-794cd65ff4-mcxtr:/#
```
