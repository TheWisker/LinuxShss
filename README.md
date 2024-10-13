<h1 align="center">LinuxShss</h1>
<div align="center">
    <a href="https://github.com/TheWisker/LinuxShss">
        <img width="400" src="./assets/logo.png">
    </a>
</div>
<p align="center">Collection of Linux shell utilities</p>

<h2 align="center">Index</h2>

<div align="center">
    
  [Description][description]
  
  [Features][features]
  
  [Screenshots][screenshots]
  
  [Installation][installation]

  [Updating][updating]
  
  [Dependencies][dependencies]

  [Configuration][configuration]

  [Discussions][discussions]

  [Contributions][contributions]

  [Documentation][documentation]

  [License][license]
  
  [Code of Conduct][coc]
  
  [Author][author]

</div>

<h2 align="center">Description [<a href="https://github.com/TheWisker/LinuxShss#index">↑</a>]</h2>

<p align="center">This is a collection of <b>Linux shell utilities</b> with each focusing on one specific task, thus following the Unix philosophy of simplicity.</p>

<h2 align="center">Features [<a href="https://github.com/TheWisker/LinuxShss#index">↑</a>]</h2>

The collection features:

- **Locrel** script to check if a list of [AUR][aur] packages and [GitHub][github] repositories have **new versions**
- **Bootrep** script to print a variety of information about the current **boot**
- **Pacup** script as a `Pacman -Syu` wrapper to nicely **prompt to update**

<h2 align="center">Screenshots [<a href="https://github.com/TheWisker/LinuxShss#index">↑</a>]</h2>

<p align="center">
  <img src="./assets/screenshots/Screenshot_One.gif"/>
</p>

<p align="center">
  <img src="./assets/screenshots/Screenshot_Two.gif"/>
</p>

<p align="center">
  <img src="./assets/screenshots/Screenshot_Three.gif"/>
</p>

<h2 align="center">Installation [<a href="https://github.com/TheWisker/LinuxShss#index">↑</a>]</h2>

<h3>Arch Linux</h3>

You can install **LinuxShss** from the [AUR][aur] repository:

<a href="https://aur.archlinux.org/packages/linuxshss">
  <img src="https://img.shields.io/aur/version/linuxshss" height=24px/>
</a>

- For information on how to install an [AUR][aur] package read [this][aur-wiki] wiki.

Then you should **ensure** the shell you use has `~/.local/bin` added to the **PATH** env.

> [!NOTE]
> Only users **created after** installation will have the scripts in `~/.local/bin` as explained in the *manual* installation instructions.

<h3>Manually</h3>

The **LinuxShss** installation is really straightforward. 

Check you have the **required** [dependencies][dependencies].
**Copy** the files located in the `./bin/` directory of the **repository** to `/etc/skel/.local/bin` and/or `~/.local/bin` to install *globally* or on a *per-user* basis.
When installed *globally*, every user **created after** the installation will receive a **copy** of the scripts in `~/.local/bin` except if the system has a *different* skel directory configured or *does not copy* the skel directory on
user creation. After installing the scripts **ensure** the shell you use has `~/.local/bin` added to the **PATH** env as to be able to directly run the scripts without having to be on the installation directory.

> [!NOTE]
> Even though the scripts can be installed to a global location like `/usr/bin` it is preffered to install them to the user path `~/.local/bin` as they are meant to be easyly customizable and some perform
> user-specific actions.

<h2 align="center">Updating [<a href="https://github.com/TheWisker/LinuxShss#index">↑</a>]</h2>

When updating **LinuxShss** just follow the steps for installation. 

> [!WARNING]
> Any **custom changes** to the scripts will **dissapear**. If you wish those changes **persist** simply add them to the **new** scripts.

<h2 align="center">Dependencies [<a href="https://github.com/TheWisker/LinuxShss#index">↑</a>]</h2>

<h3 align="left">Buildtime</h3>

The **LinuxShss** project has no *buildtime* dependencies.

<h3 align="left">Runtime</h3>

Every scripts depends on [bash][bash] as they are **bash scripts**.

- **Locrel** script also depends on [jq][jq] for **parsing** [JSON][JSON], [curl][curl] for **pulling** web data and [awk][awk] for **modifying** origins file. **Errors** will be issued if the dependencies are **not found**!
- **Bootrep** *optionally* depends on some system configuration to work and will print some errors if the system does not use what it expects to use. In such case, simply delete
the lines that print those errors as they target a **different system** configuration. If the user is knowledgeable in their system configuration they can usually replace them to work for their system.
- **Pacup** depends on [pacman][pacman] as it is fundamentally just a simple **wrapper** for prompting if the user wants to update, with a **default** value of no.

<h2 align="center">Configuration [<a href="https://github.com/TheWisker/LinuxShss#index">↑</a>]</h2>

The only **script** which actually has configuration is **Locrel** which has a `$origins` **variable** at the start of the file that contains the **path** of the origins file.

<h2 align="center">Discussions [<a href="https://github.com/TheWisker/LinuxShss#index">↑</a>]</h2>

Feel free to give any **ideas** for future **scripts** [here][discussion-ideas]
and ask any **questions** you have [here][discussion-questions].

<h2 align="center">Contributions [<a href="https://github.com/TheWisker/LinuxShss#index">↑</a>]</h2>

All contributions are welcome!
The **steps** involved when making a contribution are **explained** in the [CONTRIBUTING.md][contributing] file.
We look forward to your contributions!

- The **contributors** list is located [here][contributors].

<h2 align="center">Documentation [<a href="https://github.com/TheWisker/LinuxShss#index">↑</a>]</h2>

- **Locrel**:
  - Configure the `$origins` **variable** in the script to point to a **valid** origins file
  - **Populate** the origins file following the format:
    - \<provider\> \<identifier\> \<latest_version\> (\<branch\>)
    - Where
      - \<provider\>: ( 'aur' | 'github' | 'github-commit' )
      - \<identifier\>: ( **aur** -> *package-name* | ( **github** | **github-commit** ) -> *user/repo* )
      - \<latest_version\>: ((**aur** | **github**) -> *latest-version* | **github-commit** -> *hash* )
      - \<branch\>: ( ( **aur** | **github** ) -> *not-allowed* | **github-commit** -> *branch* ) [Default: master]
    - Examples
      - aur shikai-theme v1.5.3-1
      - github TheWisker/Shikai v1.5.3
      - github-commit TheWisker/Shikai 33220107395cfbddede8b6a679269ec71fd9bb75 master
  - Simply run the **locrel** script

- **Bootrep**:
  - Make any desired **changes** like adding or removing output instructions
  - Simply run the **bootrep** script

- **Pacup**:
  - Simply run the **pacup** script

<h2 align="center">License [<a href="https://github.com/TheWisker/LinuxShss#index">↑</a>]</h2>

<p align="center"> This project is licensed under the <a href="./LICENSE"><b>GNU GENERAL PUBLIC LICENSE v3</b></a>.</p>

<h2 align="center">Code of Conduct [<a href="https://github.com/TheWisker/LinuxShss#index">↑</a>]</h2>

<p align="center"> This project follows the <a href="./.github/CODE_OF_CONDUCT.md"><b>Contributor Covenant Code of Conduct</b></a>.</p>

<h2 align="center">Author [<a href="https://github.com/TheWisker/LinuxShss#index">↑</a>]</h2>
<div align="center">
    <a href="https://github.com/TheWisker">
        <img width="200" height="200" src="./assets/profile.png"></img>
    </a>
</div>
<h4 align="center">TheWisker</h4>

[description]: https://github.com/TheWisker/LinuxShss#description-
[features]: https://github.com/TheWisker/LinuxShss#features-
[screenshots]: https://github.com/TheWisker/LinuxShss#screenshots-
[installation]: https://github.com/TheWisker/LinuxShss#installation-
[updating]: https://github.com/TheWisker/LinuxShss#updating-
[dependencies]: https://github.com/TheWisker/LinuxShss#dependencies-
[configuration]: https://github.com/TheWisker/LinuxShss#configuration-
[discussions]: https://github.com/TheWisker/LinuxShss#discussions-
[contributions]: https://github.com/TheWisker/LinuxShss#contributions-
[documentation]: https://github.com/TheWisker/LinuxShss#documentation-
[license]: https://github.com/TheWisker/LinuxShss#license-
[coc]: https://github.com/TheWisker/LinuxShss#code-of-conduct-
[author]: https://github.com/TheWisker/LinuxShss#author-
[aur]: https://aur.archlinux.org/
[aur-wiki]: https://wiki.archlinux.org/title/Arch_User_Repository
[github]: https://github.com
[bash]: https://www.gnu.org/software/bash/
[jq]: https://jqlang.github.io/jq/
[JSON]: https://www.json.org/json-en.html
[curl]: https://curl.se/
[awk]: https://en.wikipedia.org/wiki/AWK
[pacman]: https://wiki.archlinux.org/title/Pacman
[discussion-ideas]: https://github.com/TheWisker/LinuxShss/discussions/categories/ideas
[discussion-questions]: https://github.com/TheWisker/LinuxShss/discussions/categories/q-a
[contributing]: ./CONTRIBUTING.md
[contributors]: ./CONTRIBUTORS.md