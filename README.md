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
