```
# Rutorrent plugins
execute = {sh,-c,/usr/bin/php7 /usr/share/webapps/rutorrent/php/initplugins.php abc &}
execute.nothrow = rm,/run/php/.rtorrent.sock
# SGCI
network.scgi.open_local = /run/php/.rtorrent.sock
#network.scgi.open_port = 0.0.0.0:5000

# Logging
log.open_file = "rtorrent", /config/log/rtorrent/rtorrent.log
log.add_output = "info", "rtorrent"
log.add_output = "torrent_warn", "rtorrent"
log.add_output = "tracker_warn", "rtorrent"
log.add_output = "storage_warn", "rtorrent"

# Maximum number of simultanious downloads/uploads globaly.
throttle.max_downloads.global.set = 1024
throttle.max_uploads.global.set = 1024
# Maximum number of simultanious downloads/uploads per torrent.
throttle.max_downloads.set = 256
throttle.max_uploads.set = 1024
# Maximum and minimum number of peers to connect to per torrent.
throttle.min_peers.normal.set = 1
throttle.max_peers.normal.set = 256
# Same as above but for seeding completed torrents (-1 = same as downloading)
throttle.min_peers.seed.set = 32
throttle.max_peers.seed.set = -1

# Set the numwant field sent to the tracker, which indicates how many peers we want.
# A negative value disables this feature. Default: `-1` (`tracker_numwant`)
trackers.numwant.set = 64

# Download/Upload rates
throttle.global_down.max_rate.set_kb = 0
throttle.global_up.max_rate.set_kb = 0
network.tos.set = throughput

# Session
session.path.set = /config/rtorrent/rtorrent_sess
session.use_lock.set = yes
session.on_completion.set = yes

# Schedules
schedule = socket_chmod,0,0,"execute=chmod,0660,/run/php/.rtorrent.sock"
schedule = socket_chgrp,0,0,"execute=chgrp,abc,/run/php/.rtorrent.sock"
schedule = low_diskspace,5,60,close_low_diskspace=100M
schedule = watch_directory,5,5,"load.start=/downloads/torrents/rutorrent/watched/*.torrent,d.delete_tied="

# Default directory
directory.default.set = /downloads/torrents/rutorrent/incoming

# Bind
network.bind_address.set = 0.0.0.0

# Port
network.port_range.set = 51413-51413
#network.port_random.set = no

# Hash on finish
pieces.hash.on_completion.set = no

# UDP trackers
trackers.use_udp.set = no

# Prefer encryption
protocol.encryption.set = allow_incoming,try_outgoing,enable_retry,prefer_plaintext

# DHT and peer exchange
dht.mode.set = disable
dht.port.set = 6881
protocol.pex.set = no

# Encoding
encoding_list = UTF-8

# Umask
system.umask.set = 002

# Allocate disk space
system.file.allocate.set = 0
network.max_open_files.set = 1024

# move completed downloads from incoming/ to completed/
method.insert = d.get_finished_dir, simple, "cat=/downloads/torrents/rutorrent/completed/,$d.custom1="
method.insert = d.data_path, simple, "if=(d.is_multi_file), (cat,(d.directory),/), (cat,(d.directory),/,(d.name))"
method.insert = d.move_to_complete, simple, "d.directory.set=$argument.1=; execute=mkdir,-p,$argument.1=; execute=mv,-u,$argument.0=,$argument.1=; d.save_full_session="
method.set_key = event.download.finished,move_complete,"d.move_to_complete=$d.data_path=,$d.get_finished_dir="
```