# DRipper

DESCRIPTION
-----------

This version of DRipper is forked from: https://github.com/qlspd/russia_ddos and provides possibility to run it on list of targets provided from web server.
Script receives targets in json array and tries to attack first of them, if number of successful request was less than failed in 30 seconds period it switches to next target.
When there is no mor targets, or 30 minutes elapsed, script tries to get new list of targets.

Here is original code: https://gist.github.com/scamp/33807688d0ebdcfbd4c29a4b992a8b54,
you can see there a lot of cons like extra requests to Facebook and validator.w3.com,
trying establishing connection with attacked resource (but there is no need in it if you want to send a UDP packet).
Also, the old version is inefficient: you need run several processes to have your processor busy.

## Usage

```bash

██████╗ ██████╗ ██╗██████╗ ██████╗ ███████╗██████╗
██╔══██╗██╔══██╗██║██╔══██╗██╔══██╗██╔════╝██╔══██╗
██║  ██║██████╔╝██║██████╔╝██████╔╝█████╗  ██████╔╝
██║  ██║██╔══██╗██║██╔═══╝ ██╔═══╝ ██╔══╝  ██╔══██╗
██████╔╝██║  ██║██║██║     ██║     ███████╗██║  ██║
╚═════╝ ╚═╝  ╚═╝╚═╝╚═╝     ╚═╝     ╚══════╝╚═╝  ╚═╝

It is the end user's responsibility to obey all applicable laws.
It is just like a server testing script and Your IP is visible.

Please, make sure you are ANONYMOUS!
     
Usage: python DRipper.py [options] arg

Options:
  -h, --help            show this help message and exit
  -t THREADS, --threads=THREADS
                        threads (default: 100)
  -r RANDOM_PACKET_LEN, --random_len=RANDOM_PACKET_LEN
                        Send random packets with random length (default: 1
  -l MAX_RANDOM_PACKET_LEN, --max_random_packet_len=MAX_RANDOM_PACKET_LEN
                        Max random packets length (default: 48)
  -m ATTACK_METHOD, --method=ATTACK_METHOD
                        Attack method: udp (default), http, tcp
  -c CONFIG_SERVER, --config=CONFIG_SERVER 
                        link to endpoint that provides target
Example: python DRipper.py -s 192.168.0.1 -p 80 -t 100
```

## How to Run

Ensure you have Python 3 installed. Then clone this repo and run DRipper.py with params you need
My config server is enabled by default, you can switch it by providing -c argument

```bash
git clone https://github.com/Shchava/dripper_automized.git
cd dripper_automized

# run
python DRipper.py -c 127.0.0.1/configs -t 100 -r 1 -m udp
# OR
python3 DRipper.py -c 127.0.0.1/configs -t 100 -r 1 -m udp
```

## Config server

My implementation of config server is here: https://github.com/Shchava/Dripper_config_server
Configs is provided in json format where: 
```json
    [
      {
        "address":"target address",
        "port":"target port",
        "protocol":"Attack method: udp (default), http, tcp"
      },
      ...
    ]
```
attack method form json is ignored if it was specified in run arguments

# License

This project is distributed under the MIT License, see [LICENSE](./LICENSE) for more information.
