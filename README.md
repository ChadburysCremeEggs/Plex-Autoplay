#!/usr/bin/with-contenv bash

web_client_path="$(find /usr/lib/plexmediaserver/ -name WebClient.bundle)/Contents/Resources/js"

file_to_edit=$(du -a "$web_client_path" | sort -hr | sed -n '2{p;q}' | awk '{print $2}')

if grep -q "secondsLeft:10" "$file_to_edit"; then
    echo "Removing Plex Autoplay Delay"
    sed -i 's/secondsLeft:10/secondsLeft:0/g' "$file_to_edit"
fi# Plex-Autoplay
