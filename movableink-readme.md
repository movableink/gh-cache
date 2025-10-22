# gh-cache

This is a fork of https://github.com/runs-on/cache

## Organization Variable



### Build

The build uses a tool called [ncc](https://github.com/vercel/ncc) to bundle the typescript code into a single `index.js` file. These `index.js` files are in the `dist` folder.

They can build by starting a docker container with node 20.

```
podman run -v ./:/tmp/gh-cache --entrypoint=/bin/bash -it node:20
```

Then running these commands inside the container

```
cd /tmp/gh-cache
npm install -g @vercel/ncc@0.38.3
npm install
ncc build -o dist/restore src/restore.ts && ncc build -o dist/save src/save.ts && ncc build -o dist/restore-only src/restoreOnly.ts && ncc build -o dist/save-only src/saveOnly.ts
```

(The version of ncc may be updated.)

This should output a set of four files in the `dist` folder.
