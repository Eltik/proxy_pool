# Note
Refer to [the original repo](https://github.com/Eltik/proxy_pool) for more info. This is lazily put together. All I did was add the `/proxy/` route so it will proxy requests.

# Installation
You need Python3 to run this server and Redis.

## Python3
Tutorial on installing Python.

### MacOS
Python is natively supported on MacOS. If necessary, you can use [Homebrew](https://brew.sh) to install additional Python instances, but it isn't recommended.

### Windows
You can install Python on Windows via the [official website](https://python.org).

### Linux
Use the following command to install Python3 and pip3:
```bash
sudo apt install python3-pip
```

## Redis
Tutorial on installing Redis.

### MacOS
Use [Homebrew](https://brew.sh) to install Redis:
```bash
brew install redis
```
Then:
```bash
redis-server
```
To start up the Redis server.

### Windows
TBD

### Linux
```bash
# Prerequisites
sudo apt install lsb-release

# Signing and packages and stuff
curl -fsSL https://packages.redis.io/gpg | sudo gpg --dearmor -o /usr/share/keyrings/redis-archive-keyring.gpg

echo "deb [signed-by=/usr/share/keyrings/redis-archive-keyring.gpg] https://packages.redis.io/deb $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/redis.list

# Installation
sudo apt-get update
sudo apt-get install redis

# Start
sudo redis-server

# Flushes the database
redis-cli flushall
```

## Additional Dependencies
Install Python requirements:
```bash
cd proxy_pool
pip3 install -r requirements.txt
```
In `/proxy_pool/setting.py`, edit the settings necessary. Please note the Redis setting:
```python
DB_CONN = 'redis://localhost:6379'
```

## Starting Up the Server
First run:
```bash
python3 proxyPool.py schedule
```
This will run a scheduler to fetch proxies and input them into the Redis database. If you are using Linux, I recommend using `screen python3 proxyPool.py schedule` to "keep the terminal open."
Then:
```bash
python3 proxyPool.py server
 ```
 To start up the proxy server.