
#### redis-cli build with TLS(ubuntu)
* Build the redis-cli in case the apt distribution resulting in the following issue while doing the operations with the TLS enabled cluster.

`"Error: Protocol error, got "\x15" as reply type byte"`

```bash
sudo apt-get install libssl-dev
wget https://download.redis.io/releases/redis-6.2.3.tar.gz
tar -xvf redis-6.2.3.tar.gz
cd redis-6.2.3
make redis-cli BUILD_TLS=yes MALLOC=libc
sudo cp ./src/redis-cli /usr/local/bin/


# connenting with the redis-tls-enabled cluster, port 6378 in case of memorystore instance
redis-cli -h <redis-host> --cacert ./server_ca.pem --tls -p 6378
```



#### Random key-value pair generator
```bash
# will generate the 200 random key-value pair in the redis
for i in {1..200}
do
redis-cli -h <redis-host> -p 6379 set key-$RANDOM value-$RANDOM
done
```

#### Redis cheetsheet
```bash
# it will return the integer value for the keys
dbsize
# getting all of the keys
keys *
set hello world

# memorystore connection with auth-and-tls
redis-cli -h 'redis-host' --cacert ./server_ca.pem --tls -a 'auth-string'
```