# Multi stage Docker Image

## Multistage builds are useful to anyone who has struggled to optimize Dockerfiles while keeping them easy to read and maintain.


``` docker build -t mysimpleapp:v1 . ```

> ### Uncomment second part, and comment out CMD

``` docker build -t mysimpleapp:v2 . ```

> ### Explore both images. 
> ### Why the Image size do dramatcly low for v2?