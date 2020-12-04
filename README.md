# godot-server-alpine

Godot container image based on an [Alpine image variant](https://github.com/leiter-jakab/alpine-glibc). Small image meant to host Godot game servers in the cloud.

# Resources

* [Godot Game Engine](https://godotengine.org/)
* [Kubernetes](https://kubernetes.io/)
* [Godot - Exporting for dedictated servers](https://docs.godotengine.org/en/stable/getting_started/workflow/export/exporting_for_dedicated_servers.html)

# Usage

The image is primarily meant as a base image.

```
FROM leiterjakab/godot-server-alpine

COPY --chown=godot:godot game-server.pck /godot/game-server.pck

WORKDIR /godot
USER godot
EXPOSE 9999

CMD ["./godot", "--main-pack", "game-server.pck"]
```

Fort testing purposes you can also run the container and mount the exported game package.

`docker run --rm -it --name godot-game -p 9999:9999 -v /$PWD/game-server.pck:/godot/game-server.pck -u godot leiterjakab/godot-server-alpine`

