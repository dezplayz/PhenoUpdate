# Running the Springtime Phenology Workflow in Docker

To avoid Windows compatibility issues and ensuring a robust and reproducible research environment, this guide provides detailed instructions to run the phenological modelling pipeline using Docker.

## Reasoning for Docker

The usage of Docker avoids:
- R/Python path integration problems on Windows
- SIGALRM errors in Springtime’s utils.py
- Compatibility issues with rpy2
- Complex manual setup of environments (previous Conda environment) and paths
The Linux based container instead handles all dependencies
## Requirements

### Install Windows Subsystem for Linux (WSL):

`wsl --install`

- Guide: https://learn.microsoft.com/en-us/windows/wsl/install 
- Restart and install Ubuntu if prompted.

### Install Docker Desktop

- Download: https://docs.docker.com/desktop/setup/install/windows-install/ 
- follow up the installation by signing in with a DockerHub account
- Ensure Docker is running with the WSL2 backend

### 1. Pull Springtime Docker Image

Use the official Springtime image provided by the original developers:

`docker pull ghcr.io/phenology/springtime:latest`

### 2. Start the Container

Run the container and expose port 8888 to use Jupyter notebooks to create an interactive terminal session inside the container:

`docker run -p 8888:8888 -it ghcr.io/phenology/springtime:latest`

### 3. Launch Jupyter Notebook

Inside container:

`jupyter notebook --ip=0.0.0.0 --port=8888 --allow-root`

Then, open http://localhost:8888 in your browser.

### 4. Install rpy2 inside the Container

`%pip install rpy2`

**Unlike on native Windows, this works flawlessly in Docker**

## Notes

The patched `utils.py` file used in the original replication for Windows is not needed in Docker. The platform specific issues are resolved by default when running Springtime in the Linux environment. 

## References

- Springtime Docs: https://springtime.readthedocs.io

- Docker Docs: https://docs.docker.com/desktop/

- WSL Setup: https://learn.microsoft.com/en-us/windows/wsl/install

- GitHub of original Replication: https://github.com/medh642/PhenoModel