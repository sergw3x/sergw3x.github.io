```
docker run --rm \
  --volume="$PWD/web:/srv/jekyll:Z" \
  --publish 4000:4000 \
  jekyll/jekyll:2.5 \
  jekyll serve
```