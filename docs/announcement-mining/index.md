The information in this document refers to announcement mining (also known as "ann mining", "pkt mining" or just "mining").

## How to Announcement mine (ann mine)

There are a number of options available when it comes to installing the PacketCrpyt announcement miner. Choose whichever best suits your technical ability:

### Options 1: Install a Pre-built Binary

Pre-built packetcrypt binaries (for linux) or installation packages (for macos) and archives (for windows) can be downloaded from the [packetcrypt releases page](https://github.com/cjdelisle/packetcrypt_rs/releases/).

- For **windows**, download the zip archive suffixed with `-windows.zip`  
  and extract its content.
- For **macos**, download the package suffixed with `.pkg`  
  and click on its icon in the Finder for installation.
- For **linux**, download the binary suffixed with `-linux_amd64`
  and rename it `packetcrypt`.
- - If you're on Arch linux or Manjaro, you can install the [packetcrypt AUR package](https://aur.archlinux.org/packages/packetcrypt)


### Option 2: Deploy a Docker Image

There is a PacketCrypt Docker image available, which can be used for announcement mining.

To install follow these steps:

1. Download and install [Docker](https://www.docker.com/) for your operating system.

2. Download the PacketCrypt Docker image:

```console
$ docker pull thomasjp0x42/packetcrypt
```

There are also PacketCrypt Docker images built without the portable flag (`--no-portable`) which may increase the performance of the announcement mining while reducing CPU compatibility. One such image (compiled on AMD 5950x) is available at `thomasjp0x42/packetcrypt-amd64`. Additionally, for ARM devices such as Raspberry Pi, there is an image available at `thomasjp0x42/packetcrypt-arm64`. The arm64 image will also work on Apple silicon such as the M1 and M2 chips.

3. Run the container similar to the commands described in the [Begin Announcement Mining](#begin-announcement-mining) section, except replace this part of the command:

```console
$ packetcrypt
```

with this command to run PacketCrypt from Docker:

```command
$ docker run thomasjp0x42/packetcrypt
```

The final command will be formatted like this:

```console
$ docker run thomasjp0x42/packetcrypt ann -p <your_wallet_address> <pool_1>
```

More information can be found at the [PacketCrypt DockerHub page](https://hub.docker.com/r/thomasjp0x42/packetcrypt)

### Options 3: Build From Source

Building from source will generally offer the best mining performance but requires more technical knowledge than the previous two options.

First install rust if you haven't, see: [rustup](https://rustup.rs/)

```
git clone https://github.com/cjdelisle/packetcrypt_rs
cd packetcrypt_rs
cargo build --release
```

See the [PacketCrypt GitHub repository](https://github.com/cjdelisle/packetcrypt_rs) for more detailed instructions.

---

### Begin Announcement Mining

!!! danger "Important"
    **You cannot mine into the electrum wallet**, You can only mine into the [Command Line Wallet](https://docs.pkt.cash/en/latest/pktd/pktwallet/), the [Pkt.World Wallet](https://www.pkt.world/wallet) or the [Mac GUI Wallet](https://github.com/artrepreneur/PKT-Cash-Wallet/releases) .

To begin mining, you will need the address of your wallet and you will need to choose a pool.

There are two ways to configure the announcement miner; by using CLI parameters or by using a configuration file:

**Using the CLI**

    packetcrypt ann -p <your_wallet_address> pool_1 [pool_2 pool_3 pool_4]

    [or for windows]

    packetcrypt.exe ann -p <your_wallet_address> pool_1 [pool_2 pool_3 pool_4]

**Using a Configuration File**

A configuration file must be in JSON format. The file can be loaded from the local filesystem or from a web-accessible location.

Any CLI parameters used will overide the corresponding settings in the configuration file.

Example config.json:

```
{
  "payment_addr": "<your_wallet_address>",
  "pools": [
    "pool_1",
    "pool_2",
    "pool_3",
    "pool_4"
  ]
}
```
    packetcrypt ann -c "./config.json"

    [or]

    packetcrypt ann -c "https://example.com/config.json"

    [or for windows]

    packetcrypt.exe ann -c "./config.json"

    [or]

    packetcrypt.exe ann -c "https://example.com/config.json"

Announcement mining can be done into a single pool or multiple pools. When you announcement mine into multiple pools, you will be paid by each pool that you submit announcements to.

pool_1 is the pool running the highest difficulty. If you notice problems, you can test listing the pools in a different order. The number of pools you mine into is at your discretion. If a pool is down or malfunctioning you will notice the pool is not mining at [100%] in your mining feed and you can choose to remove the under-performing or malfunctioning pool.

## How to install a PKT miner on Mac

1. Install the [Zulu](https://github.com/artrepreneur/Zulu){target=_blank} or [CLI](https://docs.pkt.cash/en/latest/pktd/pktwallet/) PKT Wallet from [https://docs.pkt.cash](https://docs.pkt.cash)
2. Download the [PacketCrypt.pkg](https://github.com/cjdelisle/packetcrypt_rs/releases/tag/packetcrypt-v0.5.0){target=_blank} for mac
3. Open your Terminal
4. Install Rust by entering in the command: ```$ curl --proto '=https' --tlsv1.2 -sSf * https://sh.rustup.rs | sh```
5. Press **1** to confirm
6. Enter the command: ```$ sudo install make```
7. Enter the command: ```$ git clone https://github.com/cjdelisle/packetcrypt_rs```
8. Enter the command: ```$ cd packetcrypt_rs```
9. Enter the command: ```$ ~/.cargo/bin/cargo build --release```
10. Enter the command: ```$ ./target/release/packetcrypt ann -p [your PKT Wallet Address] [pool 1] [pool 2] [pool 3] [pool 4] ```

## Choosing Pools to mine in

You can mine in as many pools as you have the bandwidth to supply. The same data will be uploaded so your CPU is only used once. Currently the pools which are regularly winning blocks include:

- Pkteer: `http://pool.pkteer.com`
- PKTPool: `http://pool.pktpool.io`
- PktWorld: `http://pool.pkt.world`
- Zetahash (f.k.a. Srizbi): `https://stratum.zetahash.com`

In general the recommendation is to list the pool with highest difficulty in the first position to ensure your announcements will be accepted, as the standardized policy is to accept announcements of a higher difficulty for pools with a lower base difficulty. In some cases the rewards might vary depending on the pool order regardless of difficulty, subject to custom policies implemented by the respective pools.

(Check the relevant channels on Discord for current pool statuses)

You should test your daily earnings on each pool to see which one is best. Your mining revenue depends on how much each pool allocates towards announcement miners as well as how much hardware they are using in-house. The pools are winning different blocks and if you mine to just one pool, your not getting any payment from the others when they win a block. It's the same with mining to a pool that is not winning any blocks.

---

## Limiting System Resource Usage

Limiting the system resources available to Packetcrypt may negatively effect your mining power but can be useful to conserve resources for other processess.

#### Limit CPU Usage

Announcement mining is a resource intensive process. By default, Packetcrypt will use 100% of the available CPU resources. CPU usage can be limited by assigning a limited number of threads to packetcrypt using the `-t` CLI parameter or `"threads"` key if using a configuration file.

Example of assigning four (4) threads to Packetcrypt:

```
packetcrypt ann -p <your_wallet_address> pool_1 [pool_2 pool_3 pool_4] -t 4
```

or

```
{
  "threads" 4
}
```

#### Limit Bandwidth Usage

Bandwidth usage is directly related to two main factors:

1 - Mining difficulty of the primary pool (the first pool listed in Packetcrypt pool configuration)

+ A lower difficulty means higher bandwidth usage

2 - The number of pools mined

+ Packetcrypt will send the same Announcements to each pool mined

Bandwidth usage can therefore be limited by selecting a higher difficulty pool as the primary pool and/or by mining to fewer pools.

---

## FAQ for ANN Miners

### What does overflow mean?

When the ann handler receives an announcement, it puts it into a queue, when the queue fills up it responds overflow immediately. The queue can become long, so you may receive "operation timed out" you're still being paid, when you receive "overflow" you are not being paid.

Unfortunately, you may also receive "operation timed out" because the handler is unresponsive, it's not obvious which is the reason from looking at the logs.

For example, what you will see in the AnnMiner Logs:

    1618394538 INFO annmine.rs:519 467 Ke/s   28.56Mb/s   overflow: [0, 0, 3072, 0]      uploading: [0, 0, 17632, 0]                 accept/reject: [26932/0, 0/0, 4856/0, 796/0]                    - goodrate: [100%, 100%, 61%, 100%]

-     467 Ke/s
  467 kilo-encryptions (thousands of encryptions) per second of mining power.
-     28.56Mb/s
  Total upload bandwidth (to all pools - combined)
-     overflow: [0, 0, 3072, 0]
  Overflowed the internal queue of the ann miner, before it was even able to upload to the pool, one number for each pool you're mining to.
-     3072
  Number of anns which are not uploaded to pool #3.
-     uploading [0, 0, 17632, 0]
  Number of anns currently in-flight in active http requests, again 3rd pool is a problem, others are doing well (in this example).
-     accept/reject [26932/0, 0/0, 4856/0, 796/0]
  Anns accepted/rejected by each pool, these numbers are based on the previous 10 seconds, pool #2 is giving a zero accepted which might be an issue, keep watching the next message 10 seconds later for another update.
-     goodrate [100%, 100%, 61%, 100%]
  Goodrate = number of anns accepted divided by number of anns produced.