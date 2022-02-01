---
description: >-
  The LND configuration file can be edited to customize your Lightning Network
  node.
---

# lnd.conf

The LND configuration file is found in your LND directory, typically in \~/.lnd

A sample configuration file [can be found here](https://github.com/lightningnetwork/lnd/blob/master/sample-lnd.conf) or in your local copy of the LND source code. This file exists purely for illustrative purposes, and do not serve as a template for an ["ideal"](optimal-configuration-of-a-routing-node.md) node.

{% code title="lnd.conf" %}
```javascript
; Example configuration for lnd.
;
; The default location for this file is in ~/.lnd/lnd.conf on POSIX OSes,
; $LOCALAPPDATA/Lnd/lnd.conf on Windows,
; ~/Library/Application Support/Lnd/lnd.conf on Mac OS and $home/lnd/lnd.conf on
; Plan9.
; The default location of this file can be overwritten by specifying the
; --configfile= flag when starting lnd.
;
; Boolean values can be specified as true/false or 1/0.

[Application Options]

; The directory that lnd stores all wallet, chain, and channel related data
; within The default is ~/.lnd/data on POSIX OSes, $LOCALAPPDATA/Lnd/data on
; Windows, ~/Library/Application Support/Lnd/data on Mac OS, and $home/lnd/data
; on Plan9. Environment variables are expanded so they may be used. NOTE:
; Windows environment variables are typically %VARIABLE%, but they must be
; accessed with $VARIABLE here. Also, ~ is expanded to $LOCALAPPDATA on Windows.
; datadir=~/.lnd/data

; The directory that logs are stored in. The logs are auto-rotated by default.
; Rotated logs are compressed in place.
; logdir=~/.lnd/logs

; Number of logfiles that the log rotation should keep. Setting it to 0 disables deletion of old log files.
; maxlogfiles=3
;
; Max log file size in MB before it is rotated.
; maxlogfilesize=10

; Time after which an RPCAcceptor will time out and return false if
; it hasn't yet received a response.
; acceptortimeout=15s

; Path to TLS certificate for lnd's RPC and REST services.
; tlscertpath=~/.lnd/tls.cert

; Path to TLS private key for lnd's RPC and REST services.
; tlskeypath=~/.lnd/tls.key

; Adds an extra ip to the generated certificate. Setting multiple tlsextraip= entries is allowed.
; (old tls files must be deleted if changed)
; tlsextraip=

; Adds an extra domain to the generate certificate. Setting multiple tlsextradomain= entries is allowed.
; (old tls files must be deleted if changed)
; tlsextradomain=

; If set, then all certs will automatically be refreshed if they're close to 
; expiring, or if any parameters related to extra IPs or domains in the cert 
; change.
; tlsautorefresh=true

; The duration from generating the self signed certificate to the certificate
; expiry date. Valid time units are {s, m, h}.
; The below value is about 14 months (14 * 30 * 24 = 10080)
; tlscertduration=10080h

; Do not include the interface IPs or the system hostname in TLS certificate,
; use first --tlsextradomain as Common Name instead, if set.
; tlsdisableautofill=true

; A list of domains for lnd to periodically resolve, and advertise the resolved
; IPs for the backing node. This is useful for users that only have a dynamic IP,
; or want to expose the node at a domain.
; externalhosts=my-node-domain.com

; Sets the directory to store Let's Encrypt certificates within
; letsencryptdir=~/.lnd/letsencrypt

; The IP:port on which lnd will listen for Let's Encrypt challenges. Let's
; Encrypt will always try to contact on port 80. Often non-root processes are
; not allowed to bind to ports lower than 1024. This configuration option allows
; a different port to be used, but must be used in combination with port
; forwarding from port 80. This configuration can also be used to specify
; another IP address to listen on, for example an IPv6 address.
; letsencryptlisten=localhost:8080

; Request a Let's Encrypt certificate for this domain. Note that the certificate
; is only requested and stored when the first rpc connection comes in.
; letsencryptdomain=example.com

; Disable macaroon authentication. Macaroons are used are bearer credentials to
; authenticate all RPC access. If one wishes to opt out of macaroons, uncomment
; the line below.
; no-macaroons=true

; Enable free list syncing for the default bbolt database. This will decrease
; start up time, but can result in performance degradation for very large
; databases, and also result in higher memory usage. If "free list corruption"
; is detected, then this flag may resolve things.
; sync-freelist=true

; Path to write the admin macaroon for lnd's RPC and REST services if it
; doesn't exist. This can be set if one wishes to store the admin macaroon in a
; distinct location. By default, it is stored within lnd's network directory.
; Applications that are able to read this file, gain admin macaroon access.
; adminmacaroonpath=~/.lnd/data/chain/bitcoin/simnet/admin.macaroon

; Path to write the read-only macaroon for lnd's RPC and REST services if it
; doesn't exist. This can be set if one wishes to store the read-only macaroon
; in a distinct location. The read only macaroon allows users which can read
; the file to access RPCs which don't modify the state of the daemon. By
; default, it is stored within lnd's network directory.
; readonlymacaroonpath=~/.lnd/data/chain/bitcoin/simnet/readonly.macaroon

; Path to write the invoice macaroon for lnd's RPC and REST services if it
; doesn't exist. This can be set if one wishes to store the invoice macaroon in
; a distinct location. By default, it is stored within lnd's network directory.
; The invoice macaroon allows users which can read the file to gain read and
; write access to all invoice related RPCs.
; invoicemacaroonpath=~/.lnd/data/chain/bitcoin/simnet/invoice.macaroon

; The strategy to use for selecting coins for wallet transactions. Options are
; 'largest' and 'random'.
; coin-selection-strategy=largest

; A period to wait before for closing channels with outgoing htlcs that have 
; timed out and are a result of this nodes instead payment. In addition to our 
; current block based deadline, if specified this grace period will also be taken
; into account. Valid time units are {s, m, h}.
; payments-expiration-grace-period=30s

; Specify the interfaces to listen on for p2p connections. One listen
; address per line.
; All ipv4 on port 9735:
;   listen=0.0.0.0:9735
; On all ipv4 interfaces on port 9735 and ipv6 localhost port 9736:
;   listen=0.0.0.0:9735
;   listen=[::1]:9736

; Disable listening for incoming p2p connections. This will override all
; listeners.
; nolisten=true

; Specify the interfaces to listen on for gRPC connections. One listen
; address per line.
; Only ipv4 localhost on port 10009:
;   rpclisten=localhost:10009
; On ipv4 localhost port 10009 and ipv6 port 10010:
;   rpclisten=localhost:10009
;   rpclisten=[::1]:10010
; On an Unix socket:
;   rpclisten=unix:///var/run/lnd/lnd-rpclistener.sock

; Specify the interfaces to listen on for REST connections. One listen
; address per line.
; All ipv4 interfaces on port 8080:
;   restlisten=0.0.0.0:8080
; On ipv4 localhost port 80 and 443:
;   restlisten=localhost:80
;   restlisten=localhost:443
; On an Unix socket:
;   restlisten=unix:///var/run/lnd-restlistener.sock

; A series of domains to allow cross origin access from. This controls the CORs
; policy of the REST RPC proxy.
; restcors=https://my-special-site.com

; Adding an external IP will advertise your node to the network. This signals
; that your node is available to accept incoming channels. If you don't wish to
; advertise your node, this value doesn't need to be set. Unless specified
; (with host:port notation), the default port (9735) will be added to the
; address.
; externalip=
;
; Instead of explicitly stating your external IP address, you can also enable
; UPnP or NAT-PMP support on the daemon. Both techniques will be tried and
; require proper hardware support. In order to detect this hardware support,
; `lnd` uses a dependency that retrieves the router's gateway address by using
; different built-in binaries in each platform. Therefore, it is possible that
; we are unable to detect the hardware and `lnd` will exit with an error
; indicating this. This option will automatically retrieve your external IP
; address, even after it has changed in the case of dynamic IPs, and advertise
; it to the network using the ports the daemon is listening on. This does not
; support devices behind multiple NATs.
; nat=true

; Disable REST API.
; norest=true

; Disable TLS for the REST API.
; no-rest-tls=true

; The ping interval for REST based WebSocket connections, set to 0 to disable
; sending ping messages from the server side. Valid time units are {s, m, h}.
; ws-ping-interval=30s

; The time we wait for a pong response message on REST based WebSocket
; connections before the connection is closed as inactive. Valid time units are
; {s, m, h}.
; ws-pong-wait=5s

; Shortest backoff when reconnecting to persistent peers. Valid time units are
; {s, m, h}.
; minbackoff=1s

; Longest backoff when reconnecting to persistent peers. Valid time units are
; {s, m, h}.
; maxbackoff=1h

; The timeout value for network connections in seconds, default to 120 seconds.
; Valid uints are {ms, s, m, h}.
; connectiontimeout=120s

; Debug logging level.
; Valid levels are {trace, debug, info, warn, error, critical}
; You may also specify <global-level>,<subsystem>=<level>,<subsystem2>=<level>,... 
; to set log level for individual subsystems. Use lncli debuglevel --show to 
; list available subsystems.
; debuglevel=debug,PEER=info

; Write CPU profile to the specified file.
; cpuprofile=

; Enable HTTP profiling on given port -- NOTE port must be between 1024 and
; 65536. The profile can be access at: http://localhost:<PORT>/debug/pprof/.
; profile=

; DEPRECATED: Allows the rpcserver to intentionally disconnect from peers with
; open channels. THIS FLAG WILL BE REMOVED IN 0.10.0.
; unsafe-disconnect=false

; Causes a link to replay the adds on its commitment txn after starting up, this
; enables testing of the sphinx replay logic.
; unsafe-replay=true

; The maximum number of incoming pending channels permitted per peer.
; maxpendingchannels=1

; The target location of the channel backup file.
; backupfilepath=~/.lnd/data/chain/bitcoin/simnet/channel.backup

; The maximum capacity of the block cache in bytes. Increasing this will result
; in more blocks being kept in memory but will increase performance when the
; same block is required multiple times.
; The example value below is 40 MB (1024 * 1024 * 40)
; blockcachesize=41943040

; Optional URL for external fee estimation. If no URL is specified, the method
; for fee estimation will depend on the chosen backend and network. Must be set
; for neutrino on mainnet.
; feeurl=https://nodes.lightning.computer/fees/v1/btc-fee-estimates.json

; If true, then automatic network bootstrapping will not be attempted. This
; means that your node won't attempt to automatically seek out peers on the
; network.
; nobootstrap=true

; If true, NO SEED WILL BE EXPOSED -- EVER, AND THE WALLET WILL BE ENCRYPTED
; USING THE DEFAULT PASSPHRASE. THIS FLAG IS ONLY FOR TESTING AND SHOULD NEVER
; BE USED ON MAINNET.
; noseedbackup=true

; The full path to a file (or pipe/device) that contains the password for
; unlocking the wallet; if set, no unlocking through RPC is possible and lnd
; will exit if no wallet exists or the password is incorrect; if
; wallet-unlock-allow-create is also set then lnd will ignore this flag if no
; wallet exists and allow a wallet to be created through RPC.
; wallet-unlock-password-file=/tmp/example.password

; Don't fail with an error if wallet-unlock-password-file is set but no wallet
; exists yet. Not recommended for auto-provisioned or high-security systems
; because the wallet creation RPC is unauthenticated and an attacker could
; inject a seed while lnd is in that state.
; wallet-unlock-allow-create=true

; Removes all transaction history from the on-chain wallet on startup, forcing a
; full chain rescan starting at the wallet's birthday. Implements the same
; functionality as btcwallet's dropwtxmgr command. Should be set to false after
; successful execution to avoid rescanning on every restart of lnd.
; reset-wallet-transactions=true

; The smallest channel size (in satoshis) that we should accept. Incoming
; channels smaller than this will be rejected, default value 20000.
; minchansize=

; The largest channel size (in satoshis) that we should accept. Incoming
; channels larger than this will be rejected. For non-Wumbo channels this 
; limit remains 16777215 satoshis by default as specified in BOLT-0002.
; For wumbo channels this limit is 1,000,000,000 satoshis (10 BTC).
; Set this config option explicitly to restrict your maximum channel size
; to better align with your risk tolerance
; maxchansize=

; The target number of blocks in which a cooperative close initiated by a remote
; peer should be confirmed. This target is used to estimate the starting fee
; rate that will be used during fee negotiation with the peer. This target is
; is also used for cooperative closes initiated locally if the --conf_target
; for the channel closure is not set.
; coop-close-target-confs=10

; The maximum time that is allowed to pass between receiving a channel state
; update and signing the next commitment. Setting this to a longer duration
; allows for more efficient channel operations at the cost of latency.
; channel-commit-interval=50ms

; The maximum number of channel state updates that is accumulated before signing
; a new commitment.
; channel-commit-batch-size=10

; The default max_htlc applied when opening or accepting channels. This value
; limits the number of concurrent HTLCs that the remote party can add to the
; commitment. The maximum possible value is 483.
; default-remote-max-htlcs=483

; The duration that a peer connection must be stable before attempting to send a
; channel update to re-enable or cancel a pending disables of the peer's channels
; on the network. (default: 19m0s)
; chan-enable-timeout=22m

; The duration that must elapse after first detecting that an already active 
; channel is actually inactive and sending channel update disabling it to the 
; network. The pending disable can be canceled if the peer reconnects and becomes
; stable for chan-enable-timeout before the disable update is sent.
; (default: 20m0s)
; chan-disable-timeout=22m

; The polling interval between attempts to detect if an active channel has become
; inactive due to its peer going offline. (default: 1m0s)
; chan-status-sample-interval=2m

; Disable queries from the height-hint cache to try to recover channels stuck in
; the pending close state. Disabling height hint queries may cause longer chain
; rescans, resulting in a performance hit. Unset this after channels are unstuck
; so you can get better performance again.
; height-hint-cache-query-disable=true

; The polling interval between historical graph sync attempts. Each historical
; graph sync attempt ensures we reconcile with the remote peer's graph from the
; genesis block. (default: 1h0m0s)
; historicalsyncinterval=2h

; If true, will not reply with historical data that matches the range specified
; by a remote peer's gossip_timestamp_filter. Doing so will result in lower
; memory and bandwidth requirements.
; ignore-historical-gossip-filters=true

; If true, lnd will not accept channel opening requests with non-zero push
; amounts. This should prevent accidental pushes to merchant nodes.
; rejectpush=true

; If true, lnd will not forward any HTLCs that are meant as onward payments. This
; option will still allow lnd to send HTLCs and receive HTLCs but lnd won't be
; used as a hop.
; rejecthtlc=true

; If true, will apply a randomized staggering between 0s and 30s when
; reconnecting to persistent peers on startup. The first 10 reconnections will be
; attempted instantly, regardless of the flag's value
; stagger-initial-reconnect=true

; The maximum number of blocks funds could be locked up for when forwarding
; payments. (default: 2016)
; max-cltv-expiry=2016

; The maximum percentage of total funds that can be allocated to a channel's
; commitment fee. This only applies for the initiator of the channel. Valid
; values are within [0.1, 1]. (default: 0.5)
; max-channel-fee-allocation=0.9

; The maximum fee rate in sat/vbyte that will be used for commitments of
; channels of the anchors type. Must be large enough to ensure transaction
; propagation (default: 10)
; max-commit-fee-rate-anchors=5

; A threshold defining the maximum amount of dust a given channel can have
; after which forwarding and sending dust HTLC's to and from the channel will
; fail. This amount is expressed in satoshis. (default: 500000)
; dust-threshold=1000000

; If true, lnd will abort committing a migration if it would otherwise have been
; successful. This leaves the database unmodified, and still compatible with the
; previously active version of lnd.
; dry-run-migration=true

; If true, option upfront shutdown script will be enabled. If peers that we open
; channels with support this feature, we will automatically set the script to
; which cooperative closes should be paid out to on channel open. This offers the
; partial protection of a channel peer disconnecting from us if cooperative
; close is attempted with a different script.
; enable-upfront-shutdown=true

; If true, spontaneous payments through keysend will be accepted.
; This is a temporary solution until AMP is implemented which is expected to be soon.
; This option will then become deprecated in favor of AMP.
; accept-keysend=true

; If non-zero, keysend payments are accepted but not immediately settled. If the
; payment isn't settled manually after the specified time, it is canceled
; automatically. [experimental]
; keysend-hold-time=true

; If true, spontaneous payments through AMP will be accepted. Payments to AMP
; invoices will be accepted regardless of this setting.
; accept-amp=true

; If true, we'll attempt to garbage collect canceled invoices upon start.
; gc-canceled-invoices-on-startup=true

; If true, we'll delete newly canceled invoices on the fly.
; gc-canceled-invoices-on-the-fly=true

; If true, our node will allow htlc forwards that arrive and depart on the same
; channel.
; allow-circular-route=true

; Time in milliseconds between each release of announcements to the network
; trickledelay=180000

; The number of peers that we should receive new graph updates from. This option
; can be tuned to save bandwidth for light clients or routing nodes. (default: 3)
; numgraphsyncpeers=9

; If true, lnd will start the Prometheus exporter. Prometheus flags are 
; behind a build/compile flag and are not available by default. lnd must be built 
; with the monitoring tag; `make && make install tags=monitoring` to activate them.
; prometheus.enable=true

; Specify the interface to listen on for Prometheus connections.
; prometheus.listen=0.0.0.0:8989

; The alias your node will use, which can be up to 32 UTF-8 characters in
; length.
; alias=My Lightning ☇

; The color of the node in hex format, used to customize node appearance in
; intelligence services.
; color=#3399FF


[Bitcoin]

; If the Bitcoin chain should be active. Atm, only a single chain can be
; active.
bitcoin.active=true

; The directory to store the chain's data within.
; bitcoin.chaindir=~/.lnd/data/chain/bitcoin

; Use Bitcoin's main network.
; bitcoin.mainnet=true

; Use Bitcoin's test network.
; bitcoin.testnet=true
;
; Use Bitcoin's simulation test network
bitcoin.simnet=true

; Use Bitcoin's regression test network
; bitcoin.regtest=false

; Use Bitcoin's signet test network
; bitcoin.signet=false

; Connect to a custom signet network defined by this challenge instead of using
; the global default signet test network -- Can be specified multiple times
; bitcoin.signetchallenge=

; Specify a seed node for the signet network instead of using the global default
; signet network seed nodes
; bitcoin.signetseednode=123.45.67.89

; Use the btcd back-end
bitcoin.node=btcd

; Use the bitcoind back-end
; bitcoin.node=bitcoind

; Use the neutrino (light client) back-end
; bitcoin.node=neutrino

; The default number of confirmations a channel must have before it's considered
; open. We'll require any incoming channel requests to wait this many
; confirmations before we consider the channel active.
; bitcoin.defaultchanconfs=3

; The default number of blocks we will require our channel counterparty to wait
; before accessing its funds in case of unilateral close. If this is not set, we
; will scale the value according to the channel size.
; bitcoin.defaultremotedelay=144

; The maximum number of blocks we will limit the wait that our own funds are
; encumbered by in the case when our node unilaterally closes. If a remote peer
; proposes a channel with a delay above this amount, lnd will reject the
; channel.
; bitcoin.maxlocaldelay=2016

; The smallest HTLC we are willing to accept on our channels, in millisatoshi.
; bitcoin.minhtlc=1

; The smallest HTLC we are willing to send out on our channels, in millisatoshi.
; bitcoin.minhtlcout=1000

; The base fee in millisatoshi we will charge for forwarding payments on our
; channels.
; bitcoin.basefee=1000

; The fee rate used when forwarding payments on our channels. The total fee
; charged is basefee + (amount * feerate / 1000000), where amount is the
; forwarded amount.
; bitcoin.feerate=1

; The CLTV delta we will subtract from a forwarded HTLC's timelock value.
; bitcoin.timelockdelta=40

; The seed DNS server(s) to use for initial peer discovery. Must be specified as
; a '<primary_dns>[,<soa_primary_dns>]' tuple where the SOA address is needed
; for DNS resolution through Tor but is optional for clearnet users. Multiple
; tuples can be specified, will overwrite the default seed servers.
; The default seed servers are:
;  mainnet:
;    bitcoin.dnsseed=nodes.lightning.directory,soa.nodes.lightning.directory
;    bitcoin.dnsseed=lseed.bitcoinstats.com
;  testnet:
;    bitcoin.dnsseed=test.nodes.lightning.directory,soa.nodes.lightning.directory
;
; Example for custom DNS servers:
; bitcoin.dnsseed=seed1.test.lightning
; bitcoin.dnsseed=seed2.test.lightning,soa.seed2.test.lightning


[Btcd]

; The base directory that contains the node's data, logs, configuration file,
; etc.
; btcd.dir=~/.btcd

; The host that your local btcd daemon is listening on. By default, this
; setting is assumed to be localhost with the default port for the current
; network.
; btcd.rpchost=localhost

; Username for RPC connections to btcd. By default, lnd will attempt to
; automatically obtain the credentials, so this likely won't need to be set
; (other than for simnet mode).
; btcd.rpcuser=kek

; Password for RPC connections to btcd. By default, lnd will attempt to
; automatically obtain the credentials, so this likely won't need to be set
; (other than for simnet mode).
; btcd.rpcpass=kek

; File containing the daemon's certificate file. This only needs to be set if
; the node isn't on the same host as lnd.
; btcd.rpccert=~/.btcd/rpc.cert

; The raw bytes of the daemon's PEM-encoded certificate chain which will be used
; to authenticate the RPC connection. This only needs to be set if the btcd
; node is on a remote host.
; btcd.rawrpccert=


[Bitcoind]

; The base directory that contains the node's data, logs, configuration file,
; etc.
; bitcoind.dir=~/.bitcoin

; The host that your local bitcoind daemon is listening on. By default, this
; setting is assumed to be localhost with the default port for the current
; network.
; bitcoind.rpchost=localhost

; Username for RPC connections to bitcoind. By default, lnd will attempt to
; automatically obtain the credentials, so this likely won't need to be set
; (other than for a remote bitcoind instance).
; bitcoind.rpcuser=kek

; Password for RPC connections to bitcoind. By default, lnd will attempt to
; automatically obtain the credentials, so this likely won't need to be set
; (other than for a remote bitcoind instance).
; bitcoind.rpcpass=kek

; ZMQ socket which sends rawblock and rawtx notifications from bitcoind. By
; default, lnd will attempt to automatically obtain this information, so this
; likely won't need to be set (other than for a remote bitcoind instance).
; bitcoind.zmqpubrawblock=tcp://127.0.0.1:28332
; bitcoind.zmqpubrawtx=tcp://127.0.0.1:28333

; Fee estimate mode for bitcoind. It must be either "ECONOMICAL" or "CONSERVATIVE".
; If unset, the default value is "CONSERVATIVE".
; bitcoind.estimatemode=CONSERVATIVE

; The maximum number of peers lnd will choose from the backend node to retrieve
; pruned blocks from. This only applies to pruned nodes.
; bitcoind.pruned-node-max-peers=4


[neutrino]

; Connect only to the specified peers at startup. This creates a persistent
; connection to a target peer. This is recommended as there aren't many
; neutrino compliant full nodes on the test network yet.
; neutrino.connect=

; Max number of inbound and outbound peers.
; 
; NOTE: This value is currently unused.
; neutrino.maxpeers=

; Add a peer to connect with at startup.
; neutrino.addpeer=

; How long to ban misbehaving peers. Valid time units are {s, m, h}. Minimum 1
; second.
; 
; NOTE: This value is currently unused.
; neutrino.banduration=

; Maximum allowed ban score before disconnecting and banning misbehaving peers.
; 
; NOTE: This value is currently unused.
; neutrino.banthreshold=

; DEPRECATED: Use top level 'feeurl' option. Optional URL for fee estimation. If
; a URL is not specified, static fees will be used for estimation.
; neutrino.feeurl=

; Optional filter header in height:hash format to assert the state of neutrino's
; filter header chain on startup. If the assertion does not hold, then the
; filter header chain will be re-synced from the genesis block.
; neutrino.assertfilterheader=

; Used to help identify ourselves to other bitcoin peers (default: neutrino).
; neutrino.useragentname=neutrino

; Used to help identify ourselves to other bitcoin peers (default: 0.11.0-beta).
; neutrino.useragentversion=0.11.0-beta

; The amount of time to wait before giving up on a transaction broadcast attempt.
; neutrino.broadcasttimeout=5s

; Whether compact filters fetched from the P2P network should be persisted to disk.
; neutrino.persistfilters=true

; Validate every channel in the graph during sync by downloading the containing
; block. This is the inverse of routing.assumechanvalid, meaning that for
; Neutrino the validation is turned off by default for massively increased graph
; sync performance. This speedup comes at the risk of using an unvalidated view
; of the network for routing. Overwrites the value of routing.assumechanvalid if
; Neutrino is used. (default: false)
; neutrino.validatechannels=false


[Litecoin]

; If the Litecoin chain should be active. Atm, only a single chain can be
; active.
; litecoin.active=true

; The directory to store the chain's data within.
; litecoin.chaindir=~/.lnd/data/chain/litecoin

; Use Litecoin's main network.
; litecoin.mainnet=true

; Use Litecoin's test network.
; litecoin.testnet=true
;
; Use Litecoin's simulation test network
; litecoin.simnet=true

; Use Litecoin's regression test network
; litecoin.regtest=false

; Litecoin does not support the signet test network. The options
; litecoin.signet, litecoin.signetchallenge and litecoin.signetseednode are
; only defined because the data structure is shared with bitcoind.

; Use the ltcd back-end.
litecoin.node=ltcd

; Use the litecoind back-end.
; litecoin.node=litecoind

; The default number of confirmations a channel must have before it's considered
; open. We'll require any incoming channel requests to wait this many
; confirmations before we consider the channel active.
; litecoin.defaultchanconfs=3

; The default number of blocks we will require our channel counterparty to wait
; before accessing its funds in case of unilateral close. If this is not set, we
; will scale the value according to the channel size.
; litecoin.defaultremotedelay=144

; The maximum number of blocks we will limit the wait that our own funds are
; encumbered by in the case when our node unilaterally closes. If a remote peer
; proposes a channel with a delay above this amount, lnd will reject the
; channel.
; litecoin.maxlocaldelay=2016

; The smallest HTLC we are willing to accept on our channels, in millisatoshi.
; litecoin.minhtlc=1

; The smallest HTLC we are willing to send out on our channels, in millisatoshi.
; litecoin.minhtlcout=1000

; The base fee in millisatoshi we will charge for forwarding payments on our
; channels.
; litecoin.basefee=1000

; The fee rate used when forwarding payments on our channels. The total fee
; charged is basefee + (amount * feerate / 1000000), where amount is the
; forwarded amount.
; litecoin.feerate=1

; The CLTV delta we will subtract from a forwarded HTLC's timelock value.
; litecoin.timelockdelta=576

; The seed DNS server(s) to use for initial peer discovery. Must be specified as
; a '<primary_dns>[,<soa_primary_dns>]' tuple where the SOA address is needed
; for DNS resolution through Tor but is optional for clearnet users. Multiple
; tuples can be specified, will overwrite the default seed servers.
; The default seed servers are:
;  mainnet:
;    litecoin.dnsseed=ltc.nodes.lightning.directory,soa.nodes.lightning.directory
;
; Example for custom DNS servers:
; litecoin.dnsseed=seed1.test-ltc.lightning
; litecoin.dnsseed=seed2.test-ltc.lightning,soa.seed2.test-ltc.lightning


[Ltcd]

; The base directory that contains the node's data, logs, configuration file,
; etc.
; ltcd.dir=~/.ltcd

; The host that your local ltcd daemon is listening on. By default, this
; setting is assumed to be localhost with the default port for the current
; network.
; ltcd.rpchost=localhost

; Username for RPC connections to ltcd. By default, lnd will attempt to
; automatically obtain the credentials, so this likely won't need to be set
; (other than for simnet mode).
; ltcd.rpcuser=kek

; Password for RPC connections to ltcd. By default, lnd will attempt to
; automatically obtain the credentials, so this likely won't need to be set
; (other than for simnet mode).
; ltcd.rpcpass=kek

; File containing the daemon's certificate file. This only needs to be set if
; the node isn't on the same host as lnd.
; ltcd.rpccert=~/.ltcd/rpc.cert

; The raw bytes of the daemon's PEM-encoded certificate chain which will be used
; to authenticate the RPC connection. This only needs to be set if the ltcd
; node is on a remote host.
; ltcd.rawrpccert=


[Litecoind]

; The base directory that contains the node's data, logs, configuration file,
; etc.
; litecoind.dir=~/.litecoin

; The host that your local litecoind daemon is listening on. By default, this
; setting is assumed to be localhost with the default port for the current
; network.
; litecoind.rpchost=localhost

; Username for RPC connections to litecoind. By default, lnd will attempt to
; automatically obtain the credentials, so this likely won't need to be set
; (other than for a remote litecoind instance).
; litecoind.rpcuser=kek

; Password for RPC connections to litecoind. By default, lnd will attempt to
; automatically obtain the credentials, so this likely won't need to be set
; (other than for a remote litecoind instance).
; litecoind.rpcpass=kek

; ZMQ socket which sends rawblock and rawtx notifications from litecoind. By
; default, lnd will attempt to automatically obtain this information, so this
; likely won't need to be set (other than for a remote litecoind instance).
; litecoind.zmqpubrawblock=tcp://127.0.0.1:28332
; litecoind.zmqpubrawtx=tcp://127.0.0.1:28333

; Fee estimate mode for litecoind. It must be either "ECONOMICAL" or "CONSERVATIVE".
; If unset, the default value is "CONSERVATIVE".
; litecoind.estimatemode=CONSERVATIVE

; The maximum number of peers lnd will choose from the backend node to retrieve
; pruned blocks from. This only applies to pruned nodes.
; litecoind.pruned-node-max-peers=4


[autopilot]

; If the autopilot agent should be active or not. The autopilot agent will
; attempt to automatically open up channels to put your node in an advantageous
; position within the network graph.
; autopilot.active=true

; The maximum number of channels that should be created.
; autopilot.maxchannels=5

; The fraction of total funds that should be committed to automatic channel
; establishment. For example 0.6 means that 60% of the total funds available
; within the wallet should be used to automatically establish channels. The total
; amount of attempted channels will still respect the maxchannels param.
; autopilot.allocation=0.6

; Heuristic to activate, and the weight to give it during scoring. (default:
; top_centrality:1)
; autopilot.heuristic=preferential:1

; The smallest channel that the autopilot agent should create (default: 20000)
; autopilot.minchansize=20000

; The largest channel that the autopilot agent should create (default: 16777215)
; autopilot.maxchansize=20000

; Whether the channels created by the autopilot agent should be private or not.
; Private channels won't be announced to the network.
; autopilot.private=true

; The minimum number of confirmations each of your inputs in funding transactions
; created by the autopilot agent must have. (default: 1)
; autopilot.minconfs=2

; The confirmation target (in blocks) for channels opened by autopilot. (default:
; 3)
; autopilot.conftarget=2


[tor]
; Allow outbound and inbound connections to be routed through Tor
; tor.active=true

; Allow the node to connect to non-onion services directly via clearnet. This
; allows the node operator to use direct connections to peers not running behind
; Tor, thus allowing lower latency and better connection stability.
; WARNING: This option will reveal the source IP address of the node, and should
; be used only if privacy is not a concern.
; tor.skip-proxy-for-clearnet-targets=true

; The port that Tor's exposed SOCKS5 proxy is listening on. Using Tor allows
; outbound-only connections (listening will be disabled) -- NOTE port must be
; between 1024 and 65535
; tor.socks=9050

; The DNS server as IP:PORT that Tor will use for SRV queries - NOTE must have
; TCP resolution enabled. The current active DNS server for Testnet listening is
; nodes.lightning.directory
; tor.dns=nodes.lightning.directory

; Enable Tor stream isolation by randomizing user credentials for each
; connection. With this mode active, each connection will use a new circuit.
; This means that multiple applications (other than lnd) using Tor won't be mixed
; in with lnd's traffic.
;
; This option may not be used while direct connections are enabled, since direct
; connections compromise source IP privacy by default.
; tor.streamisolation=true

; The host:port that Tor is listening on for Tor control connections (default:
; localhost:9051)
; tor.control=localhost:9091

; IP address that Tor should use as the target of the hidden service
; tor.targetipaddress=

; The password used to arrive at the HashedControlPassword for the control port.
; If provided, the HASHEDPASSWORD authentication method will be used instead of
; the SAFECOOKIE one.
; tor.password=plsdonthackme

; Automatically set up a v2 onion service to listen for inbound connections
; tor.v2=true

; Automatically set up a v3 onion service to listen for inbound connections
; tor.v3=true

; The path to the private key of the onion service being created
; tor.privatekeypath=/path/to/torkey

;The path to the private key of the watchtower onion service being created
; tor.watchtowerkeypath=/other/path/


[watchtower]

; Enable integrated watchtower listening on :9911 by default.
; watchtower.active=true

; Specify the interfaces to listen on for watchtower client connections. One
; listen address per line. If no port is specified the default port of 9911 will
; be added implicitly.
; All ipv4 on port 9911:
;   watchtower.listen=0.0.0.0:9911
; On all ipv4 interfaces on port 9911 and ipv6 localhost port 9912:
;   watchtower.listen=0.0.0.0:9911
;   watchtower.listen=[::1]:9912

; Configure the external IP address of your watchtower. Setting this field does
; not have any behavioral changes to the tower or enable any sort of discovery,
; however it will make the full URI (pubkey@host:port) available via
; WatchtowerRPC.GetInfo and `lncli tower info`.
; watchtower.externalip=1.2.3.4

; Configure the default watchtower data directory. The default directory is
; data/watchtower relative to the chosen lnddir. This can be useful if one needs
; to move the database to a separate volume with more storage. In the example
; below, the database will be stored at:
;   /path/to/towerdir/bitcoin/<network>/watchtower.db.
; watchtower.towerdir=/path/to/towerdir

; Duration the watchtower server will wait for messages to be received before
; hanging up on client connections.
; watchtower.readtimeout=15s

; Duration the watchtower server will wait for messages to be written before
; hanging up on client connections
; watchtower.writetimeout=15s


[wtclient]

; Activate Watchtower Client. To get more information or configure watchtowers
; run `lncli wtclient -h`.
; wtclient.active=true

; Specify the fee rate with which justice transactions will be signed. This fee
; rate should be chosen as a maximum fee rate one is willing to pay in order to
; sweep funds if a breach occurs while being offline. The fee rate should be
; specified in sat/byte, the default is 10 sat/byte.
; wtclient.sweep-fee-rate=10

; (Deprecated) Specifies the URIs of private watchtowers to use in backing up
; revoked states. URIs must be of the form <pubkey>@<addr>. Only 1 URI is
; supported at this time, if none are provided the tower will not be enabled.
; wtclient.private-tower-uris=


[healthcheck]

; The number of times we should attempt to query our chain backend before
; gracefully shutting down. Set this value to 0 to disable this health check.
; healthcheck.chainbackend.attempts=3

; The amount of time we allow a call to our chain backend to take before we fail
; the attempt. This value must be >= 1s.
; healthcheck.chainbackend.timeout=10s

; The amount of time we should backoff between failed attempts to query chain
; backend. This value must be >= 1s.
; healthcheck.chainbackend.backoff=30s

; The amount of time we should wait between chain backend health checks. This
; value must be >= 1m.
; healthcheck.chainbackend.interval=1m

; The minimum ratio of free disk space to total capacity that we require.
; healthcheck.diskspace.diskrequired=0.1

; The number of times we should attempt to query our available disk space before
; gracefully shutting down. Set this value to 0 to disable this health check.
; healthcheck.diskspace.attempts=2

; The amount of time we allow a query for our available disk space to take
; before we fail the attempt. This value must be >= 1s.
; healthcheck.diskspace.timeout=5s

; The amount of time we should backoff between failed attempts to query
; available disk space. This value must be >= 1s.
; healthcheck.diskspace.backoff=1m

; The amount of time we should wait between disk space health checks. This
; value must be >= 1m.
; healthcheck.diskspace.interval=6h

; The number of times we should attempt to check for certificate expiration before
; gracefully shutting down. Set this value to 0 to disable this health check.
; healthcheck.tls.attempts=2

; The amount of time we allow a query for certificate expiration to take
; before we fail the attempt. This value must be >= 1s.
; healthcheck.tls.timeout=5s

; The amount of time we should backoff between failed attempts to query
; certificate expiration. This value must be >= 1s.
; healthcheck.tls.backoff=1m

; The amount of time we should wait between certificate expiration health checks.
; This value must be >= 1m.
; healthcheck.tls.interval=1m

; The number of times we should attempt to check our tor connection before
; gracefully shutting down. Set this value to 0 to disable this health check.
; healthcheck.torconnection.attempts=3

; The amount of time we allow a call to our tor connection to take before we 
; fail the attempt. This value must be >= 1s.
; healthcheck.torconnection.timeout=10s

; The amount of time we should backoff between failed attempts to check tor 
; connection. This value must be >= 1s.
; healthcheck.torconnection.backoff=30s

; The amount of time we should wait between tor connection health checks. This
; value must be >= 1m.
; healthcheck.torconnection.interval=1m

; The number of times we should attempt to check our remote signer RPC
; connection before gracefully shutting down. Set this value to 0 to disable
; this health check.
; healthcheck.remotesigner.attempts=1

; The amount of time we allow a call to our remote signer RPC connection to take
; before we fail the attempt. This value must be >= 1s.
; healthcheck.remotesigner.timeout=1s

; The amount of time we should backoff between failed attempts to check remote
; signer RPC connection. This value must be >= 1s.
; healthcheck.remotesigner.backoff=30s

; The amount of time we should wait between remote signer RPC connection health
; checks. This value must be >= 1m.
; healthcheck.remotesigner.interval=1m


[signrpc]

; Path to the signer macaroon.
; signrpc.signermacaroonpath=~/.lnd/data/chain/bitcoin/simnet/signer.macaroon


[walletrpc]

; Path to the wallet kit macaroon.
; walletrpc.walletkitmacaroonpath=~/.lnd/data/chain/bitcoin/simnet/walletkit.macaroon


[chainrpc]

; Path to the chain notifier macaroon.
; chainrpc.notifiermacaroonpath=~/.lnd/data/chain/bitcoin/simnet/chainnotifier.macaroon


[routerrpc]

; Minimum required route success probability to attempt the payment (default:
; 0.01)
; routerrpc.minrtprob=1

; Assumed success probability of a hop in a route when no other information is
; available. (default: 0.6)
; routerrpc.apriorihopprob=0.2

; Weight of the a priori probability in success probability estimation. Valid
; values are in [0, 1]. (default: 0.5)
; routerrpc.aprioriweight=0.3

; Defines the duration after which a penalized node or channel is back at 50%
; probability (default: 1h0m0s)
; routerrpc.penaltyhalflife=2h

; The (virtual) fixed cost in sats of a failed payment attempt (default: 100)
; routerrpc.attemptcost=90

; The (virtual) proportional cost in ppm of the total amount of a failed payment
; attempt (default: 1000)
; routerrpc.attemptcostppm=900

; The maximum number of payment results that are held on disk by mission control
; (default: 1000)
; routerrpc.maxmchistory=900

; The time interval with which the MC store state is flushed to the DB.
; routerrpc.mcflushinterval=1m

; Path to the router macaroon
; routerrpc.routermacaroonpath=~/.lnd/data/chain/bitcoin/simnet/router.macaroon


[workers]

; Maximum number of concurrent read pool workers. This number should be
; proportional to the number of peers. (default: 100)
; workers.read=200

; Maximum number of concurrent write pool workers. This number should be
; proportional to the number of CPUs on the host. (default: 8)
; workers.write=8

; Maximum number of concurrent sig pool workers. This number should be
; proportional to the number of CPUs on the host. (default: 8)
; workers.sig=4


[caches]

; Maximum number of entries contained in the reject cache, which is used to speed
; up filtering of new channel announcements and channel updates from peers. Each
; entry requires 25 bytes. (default: 50000)
; caches.reject-cache-size=900000

; Maximum number of entries contained in the channel cache, which is used to
; reduce memory allocations from gossip queries from peers. Each entry requires
; roughly 2Kb. (default: 20000)
; caches.channel-cache-size=9000000

; The duration that the response to DescribeGraph should be cached for. Setting
; the value to zero disables the cache. (default: 1m)
; caches.rpc-graph-cache-duration=10m


[protocol]

; If set, then lnd will create and accept requests for channels larger than 0.16
; BTC
; protocol.wumbo-channels=true

; Set to disable support for anchor commitments. If not set, lnd will use anchor
; channels by default if the remote channel party supports them. Note that lnd
; will require 1 UTXO to be reserved for this channel type if it is enabled.
; (Deprecates the previous "protocol.anchors" setting.)
; protocol.no-anchors=true

; Set to disable support for script enforced lease channel commitments. If not
; set, lnd will accept these channels by default if the remote channel party
; proposes them. Note that lnd will require 1 UTXO to be reserved for this
; channel type if it is enabled.
; protocol.no-script-enforced-lease=true


[db]

; The selected database backend. The current default backend is "bolt". lnd
; also has experimental support for etcd, a replicated backend.
; db.backend=bolt

; The maximum interval the graph database will wait between attempting to flush
; a batch of modifications to disk. Defaults to 500 milliseconds.
; db.batch-commit-interval=500ms

; Don't use the in-memory graph cache for path finding. Much slower but uses
; less RAM. Can only be used with a bolt database backend.
; db.no-graph-cache=true

[etcd]

; Etcd database host.
; db.etcd.host=localhost:2379

; Etcd database user.
; db.etcd.user=userscopedforlnd

; Password for the database user.
; db.etcd.pass=longandsekrit

; Etcd namespace to use.
; db.etcd.namespace=lnd

; Whether to disable the use of TLS for etcd.
; db.etcd.disabletls=false

; Path to the TLS certificate for etcd RPC.
; db.etcd.cert_file=/key/path

; Path to the TLS private key for etcd RPC.
; db.etcd.key_file=/a/path

; Whether we intend to skip TLS verification
; db.etcd.insecure_skip_verify=true

; Whether to collect etcd commit stats.
; db.etcd.collect_stats=true

; If set LND will use an embedded etcd instance instead of the external one.
; Useful for testing.
; db.etcd.embedded=false

; If non zero, LND will use this as client port for the embedded etcd instance.
; db.etcd.embedded_client_port=1234

; If non zero, LND will use this as peer port for the embedded etcd instance.
; db.etcd.embedded_peer_port=1235

; If set the embedded etcd instance will log to the specified file. Useful when
; testing with embedded etcd.
; db.etcd.embedded_log_file=/path/etcd.log

; The maximum message size in bytes that we may send to etcd. Defaults to 32 MiB.
; db.etcd.max_msg_size=33554432

[postgres]
; Postgres connection string.
; db.postgres.dsn=postgres://lnd:lnd@localhost:45432/lnd?sslmode=disable

; Postgres connection timeout. Valid time units are {s, m, h}. Set to zero to
; disable.
; db.postgres.timeout=

; Postgres maximum number of connections. Set to zero for unlimited. It is
; recommended to set a limit that is below the server connection limit.
; Otherwise errors may occur in lnd under high-load conditions.
; db.postgres.maxconnections=

[bolt]

; If true, prevents the database from syncing its freelist to disk. 
; db.bolt.nofreelistsync=1

; Whether the databases used within lnd should automatically be compacted on
; every startup (and if the database has the configured minimum age). This is
; disabled by default because it requires additional disk space to be available
; during the compaction that is freed afterwards. In general compaction leads to
; smaller database files.
; db.bolt.auto-compact=true

; How long ago the last compaction of a database file must be for it to be
; considered for auto compaction again. Can be set to 0 to compact on every
; startup. (default: 168h)
; db.bolt.auto-compact-min-age=0

; Specify the timeout to be used when opening the database.
; db.bolt.dbtimeout=60s


[cluster]

; Enables leader election if set.
; cluster.enable-leader-election=true

; Leader elector to use. Valid values: "etcd" (default).
; cluster.leader-elector=etcd

; Election key prefix when using etcd leader elector. Defaults to "/leader/".
; cluster.etcd-election-prefix=/leader/

; Identifier for this node inside the cluster (used in leader election).
; Defaults to the hostname.
; cluster.id=example.com

[rpcmiddleware]

; Enable the RPC middleware interceptor functionality.
; rpcmiddleware.enable=true

; Time after which a RPC middleware intercept request will time out and return
; an error if it hasn't yet received a response.
; rpcmiddleware.intercepttimeout=2s

; Add the named middleware to the list of mandatory middlewares. All RPC
; requests are blocked/denied if any of the mandatory middlewares is not
; registered. Can be specified multiple times.
; rpcmiddleware.addmandatory=my-example-middleware
; rpcmiddleware.addmandatory=other-mandatory-middleware

[remotesigner]

; Use a remote signer for signing any on-chain related transactions or messages.
; Only recommended if local wallet is initialized as watch-only. Remote signer
; must use the same seed/root key as the local watch-only wallet but must have
; private keys.
; remotesigner.enable=true

; The remote signer's RPC host:port.
; remotesigner.rpchost=remote.signer.lnd.host:10009

; The macaroon to use for authenticating with the remote signer.
; remotesigner.macaroonpath=/path/to/remote/signer/admin.macaroon

; The TLS certificate to use for establishing the remote signer's identity.
; remotesigner.tlscertpath=/path/to/remote/signer/tls.cert

; The timeout for connecting to and signing requests with the remote signer.
; Valid time units are {s, m, h}.
; remotesigner.timeout=5s

; If a wallet with private key material already exists, migrate it into a
; watch-only wallet on first startup.
; WARNING: This cannot be undone! Make sure you have backed up your seed before
; you use this flag! All private keys will be purged from the wallet after first
; unlock with this flag!
; remotesigner.migrate-wallet-to-watch-only=true

[gossip]

; Specify a set of pinned gossip syncers, which will always be actively syncing
; whenever the corresponding peer is online. A pinned syncer does not count
; towards the configured `numgraphsyncpeers` since pinned syncers are not
; rotated. Configuring a pinned syncer does not ensure a persistent connection
; to the target peer, they will only be pinned if the connection remains active
; via some other mechanism, e.g. having an open channel.
;
; This feature is useful when trying to ensure that a node keeps its
; routing table tightly synchronized with a set of remote peers, e.g. multiple
; lightning nodes operated by the same service.
;
; Each value should be a hex-encoded pubkey of the pinned peer. Multiple pinned
; peers can be specified by setting multiple flags/fields in the config.
; gossip.pinned-syncers=pubkey1
; gossip.pinned-syncers=pubkey2

; The maximum number of updates for a specific channel and direction that lnd
; will accept over the channel update interval.
; gossip.max-channel-update-burst=10
; gossip.channel-update-interval=1m


[invoices]

; If a hold invoice has accepted htlcs that reach their expiry height and are 
; not timed out, the channel holding the htlc is force closed to resolve the
; invoice's htlcs. To prevent force closes, lnd automatically cancels these 
; invoices before they reach their expiry height.
;
; Hold expiry delta describes the number of blocks before expiry that these 
; invoices should be canceled. Setting this value to 0 will ensure that hold
; invoices can be settled right up until their expiry height, but will result
; in the channel they are on being force closed if they are not resolved before
; expiry.
; 
; Lnd goes to chain before the expiry for a htlc is reached so that there is 
; time to resolve it on chain. This value needs to be greater than the 
; DefaultIncomingBroadcastDelta set by lnd, otherwise the channel will be force
; closed anyway. A warning will be logged on startup if this value is not large
; enough to prevent force closes.
;
; invoices.holdexpirydelta=15


[routing]

; DEPRECATED: This is now turned on by default for Neutrino (use 
; neutrino.validatechannels=true to turn off) and shouldn't be used for any
; other backend!
; routing.assumechanvalid=true

; If set to true, then we'll prune a channel if only a single edge is seen as
; being stale. This results in a more compact channel graph, and also is helpful
; for neutrino nodes as it means they'll only maintain edges where both nodes are
; seen as being live from it's PoV.
; routing.strictgraphpruning=true
```
{% endcode %}

{% embed url="https://github.com/lightningnetwork/lnd/blob/master/sample-lnd.conf" %}