# Docs

![Proof HTML](https://github.com/groupplants/docs/actions/workflows/proof-html.yml/badge.svg)

Documentation for group student project based on [mkdocs](https://squidfunk.github.io/mkdocs-material/creating-your-site/#creating-your-site-unix-powershell).

## How to run

### Wisit our website

We're hosting our documentation online, here is the link:
[documetation](https://groupplants.github.io/docs/)

### Docker

1. **Install Docker**: Ensure that Docker is installed and running on your computer. You can download it from the [official Docker website](https://www.docker.com/get-started).
2. **Run the Documentation Server**:
   Use the following command to start the documentation server with Docker. This command mounts your current directory to the `/docs` directory in the container and starts the MkDocs server with the Material theme.

    ```bash
    docker run --rm -it -v ${PWD}:/docs squidfunk/mkdocs-material new .
    ```

Note: If you are using a Windows command prompt, replace `${PWD}` with `%cd%`. If you're using PowerShell, use `${PWD}`.

### Python

1. **Install Python**: Ensure that Python is installed on your computer. You can download it from the [official Python website](https://www.python.org/downloads/). It's recommended to use Python 3.6 or higher.

2. **Install Project Dependencies**:
Navigate to the project directory and install the required dependencies using the following command:

    ```bash
    python -m pip install -r requirements.txt
    ```

3. **Run the Documentation Server**:
Start the local MkDocs server using the command below. This will serve your documentation site locally and enable live reloading for changes.

    ```bash
    python -m mkdocs serve
    ```

After running this command, you should see output indicating that the server is running, and you can view your documentation in a web browser at the address provided (typically `http://127.0.0.1:8000/`).

## Creating UML schematics

### Gaphor

Download [gaphor](https://gaphor.org/download/). When creating schematics save the graphor project to the `graphor` directory.
Export them to `docs/assets/uml` - svg format.
