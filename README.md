# Phalcon + Rector in docker
Docker containers with Phalcon and Rector installed for easily scanning your project.

Create a `rector.yml` file in the root of your project containing the directories that need to be scanned and the directories that need to be autoloaded.

For example:
```
parameters:
  paths:
    - 'app'
    - 'public'
  autoload_paths:
    - 'app'
```

**Phalcon 3.4 -> Phalcon 4**

Run inside your project:
```
docker run -v $(pwd):/project ruudboon/phalcon-rector:php73-v3_to_v4
```
You will get an overview of suggested changes.
If you want to apply these changes by rector run:
```
docker run -v $(pwd):/project ruudboon/phalcon-rector:php73-v3_to_v4 process --set phalcon40
```

**PHP 7.4 - Phalcon 4**

Need to check if your interfaces align and you are 7.4 compatible? 

Run:
```
docker run -v $(pwd):/project ruudboon/phalcon-rector:php74-v4 process --set phalcon40
```
