
# voXel

**voXel** is a Docker-based application requiring Docker Desktop with WSL2 support on Windows.

---

## Requirements

- Docker Desktop (with WSL2 integration enabled)
- WSL2 Terminal on Windows

---

## Configuration

Create a `.env` file in the project directory with the following environment variables:

```env
WO_HOST=localhost
WO_PORT=8000
WO_MEDIA_DIR=appmedia
WO_DB_DIR=dbdata
WO_SSL=NO
WO_SSL_KEY=
WO_SSL_CERT=
WO_SSL_INSECURE_PORT_REDIRECT=80
WO_DEBUG=NO
WO_DEV=NO
WO_BROKER=redis://broker
WO_DEFAULT_NODES=1
WO_SETTINGS=
````

---

## Installation & Running

```bash
# Clone the repository
git clone https://github.com/neelkalpa/voXel 

# Change to the project directory
cd voXel

# Install dos2unix if not installed (fix Windows/WSL line ending issues)
sudo apt update
sudo apt install -y dos2unix

# Convert scripts to Unix line endings
dos2unix voXel.sh wait-for-it.sh wait-for-postgres.sh devenv.sh dev-worker.sh worker.sh

# Make the startup script executable
chmod +x voXel.sh

# Start voXel in development mode
./voXel.sh start --dev
```


## Adding a Processing Node

To create or restart the processing node container:

```bash
docker stop nodeodm
docker rm nodeodm
docker run -d --name nodeodm --network voxel_default -p 3000:3000 opendronemap/nodeodm
```

---

## Adding the Node from the Dashboard

1. Open the voXel WebODM dashboard in your browser at `http://localhost:8000`.
2. Navigate to the **Nodes** section or settings area where you can manage processing nodes.
3. Click **Add Node**.
4. Enter the following details for the node:
    - **Hostname:** `nodeodm`    
    - **Port:** `3000`
5. Save the node configuration.
6. The dashboard should now recognize the processing node and display its status.

---

## Notes

- Ensure Docker Desktop is running with WSL2 backend.
- The application will run on the host and port specified by `WO_HOST` and `WO_PORT`.
- Media and database directories will be mapped according to the `.env` file.

---
