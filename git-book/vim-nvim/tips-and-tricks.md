# Tips and tricks

## Sync folder

```bash
#!/bin/bash

# Synchroize files on modifications

set -euo pipefail

if [ $# -ne 2 ]; then
  echo "Usage: sync.sh ROOT_PROJECT_DIR DEST_HOST"
  echo "Example: sync.sh ~/src/erx-imcu-dkms ansible@192.168.55.1"
  exit 1
fi

src_dir=$1
host=$2

destination="$(basename $(readlink -f ${PWD}/$1))"
destination_arg="${host}:${destination}/"

# TODO this should be parameters
# C
include="src/*.c src/include/*.h src/Makefile src/Kbuild"
# Python
include="${include} pyproject.toml src/*.py"

echo "Synchronizing ${PWD}/$1 to ${destination_arg}"

# Wait for files to be modified
while inotifywait -e modify -r ${PWD}/$1/*; do
  clear
  sleep 0.5
  # Synchronize
  rsync -v ${include} --cvs-exclude -a "${src_dir}" "${destination_arg}"
  echo "Synchronized $1 with ${destination_arg}"
done
```
