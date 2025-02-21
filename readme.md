![](https://chia.net/img/chia_logo.svg)

# Chia Docker Container
https://www.chia.net/

## Configuration
Required configuration:
* Publish p2p network port via `-p 8444:8444`
* Bind mounting a host plot dir in the container to `/plots`  (e.g. `-v /path/to/hdd/storage/:/plots`)
* Bind mounting a host config dir in the container to `/root/.chia`  (e.g. `-v /path/to/storage/:/root/.chia`)
* Set initial `chia keys add` method:
  * Manual input from docker shell via `-e KEYS=type` (recommended)
  * Copy from existing farmer via `-e KEYS=copy` and `-e CA=/path/to/mainnet/config/ssl/ca/` 
  * Add key from mnemonic text file via `-e KEYS=/path/to/mnemonic.txt`
  * Generate new keys (default)

Optional configuration:
* Pass multiple plot directories via PATH-style colon-separated directories (.e.g. `-e plots_dir=/plots/01:/plots/02:/plots/03`)
* Set desired time zone via environment (e.g. `-e TZ=Europe/Berlin`)
* Publish RPC network port via `-p 8555:8555`

On first start with recommended `-e KEYS=type`:
* Open docker shell `docker exec -it <containerid> sh`
* Enter `chia keys add`
* Paste space-separated mnemonic words
* Enter `chia wallet show`
* Press `S` to skip restore from backup
* Restart docker cotainer

## Operation
* Open docker shell `docker exec -it <containerid> sh`
* Check synchronization `chia show -s -c`
* Check farming `chia farm summary`
* Check balance `chia wallet show` 
