# Trilium LazyCat community package

Upstream https://github.com/TriliumNext/Trilium (AGPL-3.0), v0.106.1. Package `community.lazycat.app.trilium`, min OS 1.5.0, amd64, mirror delivery, community (喵喵) store only. The official `in.zhaoj.trilium` and `in.zhaoj.triliumnext` entries are separate builds; this is an independent community package for TriliumNext.

Single container with the built-in encrypted SQLite database. Everything the server writes lives in one bind:

    /lzcapp/var/data:/data

The image starts as root and its own entrypoint drops to the upstream `node` account (uid 1000), but that entrypoint only chowns `/home/node`. The `setup_script` therefore creates and chowns `/data` to the same original uid/gid; the runtime identity is not overridden and no extra healthcheck, smoke test or startup gate is added.

First run shows Trilium's own setup wizard (language, then create a new knowledge base). The vault password is chosen by the user in the browser and is not derived from the LazyCat account, so this package ships no deploy parameters and no login autofill — the note tree has no headless client API that would justify one.

No `public_path` is declared: the whole app stays behind the platform entry login.

License: AGPL-3.0. The full text is bundled at `/package-licenses/COPYING.txt`. Image is used unmodified from upstream; the icon is only resized from the upstream app icon.

Not device-tested: setup wizard, vault password creation, note CRUD, import/export, scripting, sync, and persistence across restarts.
