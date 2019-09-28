# Chapter1 - Setup the application.

## Download docker
### For mac users
[Install Docker Desktop for Mac](https://docs.docker.com/docker-for-mac/install/)
### For windows users
[Install Docker Desktop on Windows](https://docs.docker.com/docker-for-windows/install/)

## Why Docker?
- ==**Reduce development environment setup time.**== Environment construction takes time because it differs depending on the OS(Mac and Windows).
- ==**To make the development environment consistent.**== Problems arise with different library versions. `For example, John downloaded Rails6 and Tim downloaded Rails5.`


## Cloning the repo
`terminal`
```bash
git clone https://github.com/KohheePeace/rails6-docker-test2.git
cd rails6-docker-test2
docker-compose up
docker-compose run web yarn install
docker-compose run web rake db:create
docker-compose run web rake db:migrate
```

## Check it works correctly
Visit `http://localhost:3000`
![Screenshot](img/chap01-localhost-3000.png)

## Useful Links

### Docker link
https://stackoverflow.com/questions/39988844/docker-compose-up-vs-docker-compose-up-build-vs-docker-compose-build-no-cach/39988980
https://github.com/rails/webpacker/blob/master/docs/docker.md