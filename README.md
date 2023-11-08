# sqwab
This is a helper project for custom builds of the [official SQLite WASM library](https://sqlite.org/wasm/doc/trunk/index.md). It allows overriding Makefile settings and adding C code without creating your own build environment.

To use it:

* Fork or clone this repo.
* Add or edit files under [overlay/ext/wasm](https://github.com/rhashimoto/sqwab/tree/master/overlay/ext/wasm) (in your fork). This will typically be one of both of:
  * Adding a modified [ext/wasm/GNUMakefile](https://sqlite.org/src/file?name=ext/wasm/GNUmakefile&ci=trunk), e.g. to change build options.
  * Using the [ext/wasm/sqlite3_wasm_extra_init.c](https://sqlite.org/src/info?name=0e362f3fc04eab6628cbe4f1e35f4ab4a200881f6b5f753b27fb45eabeddd9d2&ln=216-237) extension point to add C code.
* Once your changes are on GitHub, [manually run the workflow](https://docs.github.com/en/actions/using-workflows/manually-running-a-workflow) named "Build workflow". You will be prompted for these options:
  * Source tarball URL - Enter a source code tarball link (see the [SQLite repo home](https://sqlite.org/src/doc/trunk/README.md) under "Obtaining the SQLite Source Code"). By default this is the latest release.
  * Emscripten SDK version - This is the [Emscripten toolchain]([url](https://emscripten.org/docs/tools_reference/emsdk.html)https://emscripten.org/docs/tools_reference/emsdk.html) version. By default, this is something close to current when I created the workflow.
* A successful run of the workflow will produce a new [GitHub release]([url](https://docs.github.com/en/repositories/releasing-projects-on-github)https://docs.github.com/en/repositories/releasing-projects-on-github) on your fork with a zip file containing the built artifacts.

If you want to change the workflow itself, it is under .github/workflows/build.yml.

If the build workflow fails with an error like `HTTP 403: Resource not accessible by integration`, you may need to change your [GitHub Actions permissions](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/enabling-features-for-your-repository/managing-github-actions-settings-for-a-repository#managing-github-actions-permissions-for-your-repository). Make sure that "Workflow permissions" is set to "Read and write permissions".
