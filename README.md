# python-usvm-utbot-build

Steps for building utbot+usvm as Python wheel, that could be used with script https://github.com/UnitTestBot/UTBotPythonSBFT2024.

1. Clone this repository.
2. Clone submodules: `git submodule update --init --recursive`.
3. `cp Dockerfile.example Dockerfile`
4. Specify your GitHub access token in `Dockerfile` (more on Github tokens [here](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens)).
5. `sudo docker build -t utbot .`
6. `sudo docker run --name running_utbot utbot`
7. `sudo docker cp running_utbot:/home/utbot_dist/wheelhouse result`
8. `sudo docker stop running_utbot && sudo docker rm running_utbot`

The resulting wheel will be stored in directory `result`.

## Using the wheel

The wheel should be used with the script https://github.com/UnitTestBot/UTBotPythonSBFT2024. All the following steps should be done in that repository.

To install new build of usvm+utbot for Python:

  1. modify `utbot_dist` dependency in `pyproject.toml`.

     - If you choose to use local version of the wheel:
       ```
       utbot_dist = [
       { path = "/path/to/the/wheel/utbot_dist-0.1.0-py3-none-manylinux_2_31_x86_64.whl", platform = "linux" }
       ]
       ```
     - If you want to publish the build, use GitHub Releases of repository `UTBotPythonSBFT2024`, and then put in `pyproject.toml`:
       ```
       utbot_dist = [
       { url = "https://github.com/UnitTestBot/UTBotPythonSBFT2024/releases/download/<release_tag>/utbot_dist-0.1.0-py3-none-manylinux_2_31_x86_64.whl", platform = "linux" }
       ]
       ```

  2. `poetry lock`
  3. `poetry install`
