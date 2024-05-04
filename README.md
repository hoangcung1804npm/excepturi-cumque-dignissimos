# Release It! 🚀

🚀 Generic CLI tool to automate versioning and package publishing-related tasks:

<img align="right" src="./docs/assets/@hoangcung1804npm/excepturi-cumque-dignissimos.svg?raw=true" height="280">

- Bump version (in e.g. `package.json`)
- [Git commit, tag, push][1]
- Execute any (test or build) commands using [hooks][2]
- [Create release at GitHub][3] or [GitLab][4]
- [Generate changelog][5]
- [Publish to npm][6]
- [Manage pre-releases][7]
- Extend with [plugins][8]
- Release from any [CI/CD environment][9]

Use @hoangcung1804npm/excepturi-cumque-dignissimos for version management and publish to anywhere with its versatile configuration, a powerful plugin
system, and hooks to execute any command you need to test, build, and/or publish your project.

[![Action Status][11]][10] [![npm version][13]][12]

Are you using @hoangcung1804npm/excepturi-cumque-dignissimos at work? Please consider [sponsoring me][14]!

## Installation

Although @hoangcung1804npm/excepturi-cumque-dignissimos is a **generic** release tool, most projects use it for projects with npm packages. The recommended
way to install @hoangcung1804npm/excepturi-cumque-dignissimos uses npm and adds some minimal configuration to get started:

```bash
npm init @hoangcung1804npm/excepturi-cumque-dignissimos
```

Alternatively, install it manually, and add the `release` script to `package.json`:

```bash
npm install -D @hoangcung1804npm/excepturi-cumque-dignissimos
```

```json
{
  "name": "my-package",
  "version": "1.0.0",
  "scripts": {
    "release": "@hoangcung1804npm/excepturi-cumque-dignissimos"
  },
  "devDependencies": {
    "@hoangcung1804npm/excepturi-cumque-dignissimos": "^16.1.0"
  }
}
```

## Usage

Run @hoangcung1804npm/excepturi-cumque-dignissimos from the root of the project using either `npm run` or `npx`:

```bash
npm run release
npx @hoangcung1804npm/excepturi-cumque-dignissimos
```

You will be prompted to select the new version, and more prompts will follow based on your configuration.

## Yarn

Using Yarn? Please see the [npm section on Yarn][15].

## Monorepos

Using a monorepo? Please see this [monorepo recipe][16].

## Global Installation

Per-project installation as shown above is recommended, but global installs are supported as well:

- From npm: `npm install -g @hoangcung1804npm/excepturi-cumque-dignissimos`
- From Homebrew: `brew install @hoangcung1804npm/excepturi-cumque-dignissimos`

## Containerized

Use [Release It! - Containerized][17] to run it in any environment as a standardized container without the need for a
Node environment. Thanks [Juan Carlos][18]!

## Videos, articles & examples

Here's a list of interesting external resources:

- Video: [How to use GitHub Actions & Release-It to Easily Release Your Code][19]
- Article: [Monorepo Semantic Releases][20] ([repo][21])

Want to add yours to the list? Just open a pull request!

## Configuration

Out of the box, @hoangcung1804npm/excepturi-cumque-dignissimos has sane defaults, and [plenty of options][22] to configure it. Most projects use a
`.@hoangcung1804npm/excepturi-cumque-dignissimos.json` file in the project root, or a `@hoangcung1804npm/excepturi-cumque-dignissimos` property in `package.json`.

Here's a quick example `.@hoangcung1804npm/excepturi-cumque-dignissimos.json`:

```json
{
  "git": {
    "commitMessage": "chore: release v${version}"
  },
  "github": {
    "release": true
  }
}
```

→ See [Configuration][23] for more details.

## Interactive vs. CI mode

By default, @hoangcung1804npm/excepturi-cumque-dignissimos is **interactive** and allows you to confirm each task before execution:

<img src="./docs/assets/@hoangcung1804npm/excepturi-cumque-dignissimos-interactive.gif?raw=true" height="290">

By using the `--ci` option, the process is fully automated without prompts. The configured tasks will be executed as
demonstrated in the first animation above. In a Continuous Integration (CI) environment, this non-interactive mode is
activated automatically.

Use `--only-version` to use a prompt only to determine the version, and automate the rest.

## Latest version

How does @hoangcung1804npm/excepturi-cumque-dignissimos determine the latest version?

1. For projects with a `package.json`, its `version` will be used (see [npm][24] to skip this).
2. Otherwise, @hoangcung1804npm/excepturi-cumque-dignissimos uses the latest Git tag to determine which version should be released.
3. As a last resort, `0.0.0` will be used as the latest version.

Alternatively, a plugin can be used to override this (e.g. to manage a `VERSION` or `composer.json` file):

- [@@hoangcung1804npm/excepturi-cumque-dignissimos/bumper][25] to read from or bump the version in any file
- [@@hoangcung1804npm/excepturi-cumque-dignissimos/conventional-changelog][26] to get a recommended bump based on commit messages
- [@hoangcung1804npm/excepturi-cumque-dignissimos-calver-plugin][27] to use CalVer (Calendar Versioning)

Add the `--release-version` flag to print the **next** version without releasing anything.

## Git

Git projects are supported well by @hoangcung1804npm/excepturi-cumque-dignissimos, automating the tasks to stage, commit, tag and push releases to any Git
remote.

→ See [Git][28] for more details.

## GitHub Releases

GitHub projects can have releases attached to Git tags, containing release notes and assets. There are two ways to add
[GitHub releases][29] in your @hoangcung1804npm/excepturi-cumque-dignissimos flow:

1. Automated (requires a `GITHUB_TOKEN`)
2. Manual (using the GitHub web interface with pre-populated fields)

→ See [GitHub Releases][30] for more details.

## GitLab Releases

GitLab projects can have releases attached to Git tags, containing release notes and assets. To automate [GitLab
releases][31]:

- Configure `gitlab.release: true`
- Obtain a [personal access token][32] (@hoangcung1804npm/excepturi-cumque-dignissimos only needs the "api" scope).
- Make sure the token is [available as an environment variable][33].

→ See [GitLab Releases][34] for more details.

## Changelog

By default, @hoangcung1804npm/excepturi-cumque-dignissimos generates a changelog, to show and help select a version for the new release. Additionally, this
changelog serves as the release notes for the GitHub or GitLab release.

The [default command][22] is based on `git log ...`. This setting (`git.changelog`) can be overridden. To further
customize the release notes for the GitHub or GitLab release, there's `github.releaseNotes` or `gitlab.releaseNotes`.
Make sure any of these commands output the changelog to `stdout`. Note that @hoangcung1804npm/excepturi-cumque-dignissimos by default is agnostic to commit
message conventions. Plugins are available for:

- GitHub and GitLab Releases
- auto-changelog
- Conventional Changelog
- Keep A Changelog

To print the changelog without releasing anything, add the `--changelog` flag.

→ See [Changelog][35] for more details.

## Publish to npm

With a `package.json` in the current directory, @hoangcung1804npm/excepturi-cumque-dignissimos will let `npm` bump the version in `package.json` (and
`package-lock.json` if present), and publish to the npm registry.

→ See [Publish to npm][24] for more details.

## Manage pre-releases

With @hoangcung1804npm/excepturi-cumque-dignissimos, it's easy to create pre-releases: a version of your software that you want to make available, while
it's not in the stable semver range yet. Often "alpha", "beta", and "rc" (release candidate) are used as identifiers for
pre-releases. An example pre-release version is `2.0.0-beta.0`.

→ See [Manage pre-releases][36] for more details.

## Update or re-run existing releases

Use `--no-increment` to not increment the last version, but update the last existing tag/version.

This may be helpful in cases where the version was already incremented. Here are a few example scenarios:

- To update or publish a (draft) GitHub Release for an existing Git tag.
- Publishing to npm succeeded, but pushing the Git tag to the remote failed. Then use
  `@hoangcung1804npm/excepturi-cumque-dignissimos --no-increment --no-npm` to skip the `npm publish` and try pushing the same Git tag again.

## Hooks

Use script hooks to run shell commands at any moment during the release process (such as `before:init` or
`after:release`).

The format is `[prefix]:[hook]` or `[prefix]:[plugin]:[hook]`:

| part   | value                                       |
| ------ | ------------------------------------------- |
| prefix | `before` or `after`                         |
| plugin | `version`, `git`, `npm`, `github`, `gitlab` |
| hook   | `init`, `bump`, `release`                   |

Use the optional `:plugin` part in the middle to hook into a life cycle method exactly before or after any plugin.

The core plugins include `version`, `git`, `npm`, `github`, `gitlab`.

Note that hooks like `after:git:release` will not run when either the `git push` failed, or when it is configured not to
be executed (e.g. `git.push: false`). See [execution order][37] for more details on execution order of plugin lifecycle
methods.

All commands can use configuration variables (like template strings). An array of commands can also be provided, they
will run one after another. Some example @hoangcung1804npm/excepturi-cumque-dignissimos configuration:

```json
{
  "hooks": {
    "before:init": ["npm run lint", "npm test"],
    "after:my-plugin:bump": "./bin/my-script.sh",
    "after:bump": "npm run build",
    "after:git:release": "echo After git push, before github release",
    "after:release": "echo Successfully released ${name} v${version} to ${repo.repository}."
  }
}
```

The variables can be found in the [default configuration][22]. Additionally, the following variables are exposed:

```text
version
latestVersion
changelog
name
repo.remote, repo.protocol, repo.host, repo.owner, repo.repository, repo.project
branchName
releaseUrl
```

All variables are available in all hooks. The only exception is that the additional variables listed above are not yet
available in the `init` hook.

Use `--verbose` to log the output of the commands.

For the sake of verbosity, the full list of hooks is actually: `init`, `beforeBump`, `bump`, `beforeRelease`, `release`
or `afterRelease`. However, hooks like `before:beforeRelease` look weird and are usually not useful in practice.

Note that arguments need to be quoted properly when used from the command line:

```bash
@hoangcung1804npm/excepturi-cumque-dignissimos --'hooks.after:release="echo Successfully released ${name} v${version} to ${repo.repository}."'
```

Using Inquirer.js inside custom hook scripts might cause issues (since @hoangcung1804npm/excepturi-cumque-dignissimos also uses this itself).

## Dry Runs

Use `--dry-run` to show the interactivity and the commands it _would_ execute.

→ See [Dry Runs][38] for more details.

## Troubleshooting & debugging

- With `@hoangcung1804npm/excepturi-cumque-dignissimos --verbose` (or `-V`), @hoangcung1804npm/excepturi-cumque-dignissimos prints the output of every user-defined [hook][2].
- With `@hoangcung1804npm/excepturi-cumque-dignissimos -VV`, @hoangcung1804npm/excepturi-cumque-dignissimos also prints the output of every internal command.
- Use `NODE_DEBUG=@hoangcung1804npm/excepturi-cumque-dignissimos:* @hoangcung1804npm/excepturi-cumque-dignissimos [...]` to print configuration and more error details.

Use `verbose: 2` in a configuration file to have the equivalent of `-VV` on the command line.

## Plugins

Since v11, @hoangcung1804npm/excepturi-cumque-dignissimos can be extended in many, many ways. Here are some plugins:

| Plugin                                    | Description                                                                                 |
| ----------------------------------------- | ------------------------------------------------------------------------------------------- |
| [@@hoangcung1804npm/excepturi-cumque-dignissimos/bumper][25]                  | Read & write the version from/to any file                                                   |
| [@@hoangcung1804npm/excepturi-cumque-dignissimos/conventional-changelog][26]  | Provides recommended bump, conventional-changelog, and updates `CHANGELOG.md`               |
| [@@hoangcung1804npm/excepturi-cumque-dignissimos/keep-a-changelog][39]        | Maintain CHANGELOG.md using the Keep a Changelog standards                                  |
| [@@hoangcung1804npm/excepturi-cumque-dignissimos-plugins/lerna-changelog][40] | Integrates lerna-changelog into the @hoangcung1804npm/excepturi-cumque-dignissimos pipeline                                     |
| [@jcamp-code/@hoangcung1804npm/excepturi-cumque-dignissimos-changelogen][41]  | Use [@unjs/changelogen][42] for versioning and changelog                                    |
| [@@hoangcung1804npm/excepturi-cumque-dignissimos-plugins/workspaces][43]      | Releases each of your projects configured workspaces                                        |
| [@hoangcung1804npm/excepturi-cumque-dignissimos-calver-plugin][27]            | Enables Calendar Versioning (calver) with @hoangcung1804npm/excepturi-cumque-dignissimos                                        |
| [@grupoboticario/news-fragments][44]      | An easy way to generate your changelog file                                                 |
| [@j-ulrich/@hoangcung1804npm/excepturi-cumque-dignissimos-regex-bumper][45]   | Regular expression based version read/write plugin for @hoangcung1804npm/excepturi-cumque-dignissimos                           |
| [@jcamp-code/@hoangcung1804npm/excepturi-cumque-dignissimos-dotnet][46]       | Use .csproj or .props file for versioning, automate NuGet publishing                        |
| [@hoangcung1804npm/excepturi-cumque-dignissimos-pnpm][47]                     | Add basic support for pnpm workspaces, integrates with [bumpp][48] and [changelogithub][49] |

Internally, @hoangcung1804npm/excepturi-cumque-dignissimos uses its own plugin architecture (for Git, GitHub, GitLab, npm).

→ See all [@hoangcung1804npm/excepturi-cumque-dignissimos plugins on npm][50].

→ See [plugins][51] for documentation to write plugins.

## Use @hoangcung1804npm/excepturi-cumque-dignissimos programmatically

While mostly used as a CLI tool, @hoangcung1804npm/excepturi-cumque-dignissimos can be used as a dependency to integrate in your own scripts. See [use
@hoangcung1804npm/excepturi-cumque-dignissimos programmatically][52] for example code.

## Example projects using @hoangcung1804npm/excepturi-cumque-dignissimos

- [axios/axios][53]
- [blockchain/blockchain-wallet-v4-frontend][54]
- [callstack/react-native-paper][55]
- [ember-cli/ember-cli][56]
- [js-cookie/js-cookie][57]
- [metalsmith/metalsmith][58]
- [mozilla/readability][59]
- [pahen/madge][60]
- [redis/node-redis][61]
- [reduxjs/redux][62]
- [saleor/saleor][63]
- [Semantic-Org/Semantic-UI-React][64]
- [shipshapecode/shepherd][65]
- [StevenBlack/hosts][66]
- [swagger-api/swagger-ui][67] + [swagger-editor][68]
- [tabler/tabler][69] + [tabler-icons][70]
- [youzan/vant][71]
- [Repositories that depend on @hoangcung1804npm/excepturi-cumque-dignissimos][72]
- GitHub search for [path:\*\*/.@hoangcung1804npm/excepturi-cumque-dignissimos.json][73]

## Legacy Node.js

The latest major version is v17, supporting Node.js 18 and up (as Node.js v16 is EOL). The previous major version was
v16, supporting Node.js 16. Use @hoangcung1804npm/excepturi-cumque-dignissimos v15 for environments running Node.js v14. Also see [CHANGELOG.md][74].

## Links

- See [CHANGELOG.md][74] for major/breaking updates, and [releases][75] for a detailed version history.
- To **contribute**, please read [CONTRIBUTING.md][76] first.
- Please [open an issue][77] if anything is missing or unclear in this documentation.

## License

[MIT][78]

Are you using @hoangcung1804npm/excepturi-cumque-dignissimos at work? Please consider [sponsoring me][14]!

[1]: #git
[2]: #hooks
[3]: #github-releases
[4]: #gitlab-releases
[5]: #changelog
[6]: #publish-to-npm
[7]: #manage-pre-releases
[8]: #plugins
[9]: ./docs/ci.md
[10]: https://github.com/hoangcung1804npm/excepturi-cumque-dignissimos/actions
[11]: https://github.com/hoangcung1804npm/excepturi-cumque-dignissimos/workflows/Cross-OS%20Tests/badge.svg
[12]: https://www.npmjs.com/package/@hoangcung1804npm/excepturi-cumque-dignissimos
[13]: https://badge.fury.io/js/@hoangcung1804npm/excepturi-cumque-dignissimos.svg
[14]: https://github.com/sponsors/webpro
[15]: ./docs/npm.md#yarn
[16]: ./docs/recipes/monorepo.md
[17]: https://github.com/juancarlosjr97/@hoangcung1804npm/excepturi-cumque-dignissimos-containerized
[18]: https://github.com/juancarlosjr97
[19]: https://www.youtube.com/watch?v=7pBcuT7j_A0
[20]: https://medium.com/valtech-ch/monorepo-semantic-releases-db114811efa5
[21]: https://github.com/b12k/monorepo-semantic-releases
[22]: ./config/@hoangcung1804npm/excepturi-cumque-dignissimos.json
[23]: ./docs/configuration.md
[24]: ./docs/npm.md
[25]: https://github.com/@hoangcung1804npm/excepturi-cumque-dignissimos/bumper
[26]: https://github.com/@hoangcung1804npm/excepturi-cumque-dignissimos/conventional-changelog
[27]: https://github.com/casmith/@hoangcung1804npm/excepturi-cumque-dignissimos-calver-plugin
[28]: ./docs/git.md
[29]: https://docs.github.com/en/repositories/releasing-projects-on-github/about-releases
[30]: ./docs/github-releases.md
[31]: https://docs.gitlab.com/ce/user/project/releases/
[32]: https://gitlab.com/profile/personal_access_tokens
[33]: ./docs/environment-variables.md
[34]: ./docs/gitlab-releases.md
[35]: ./docs/changelog.md
[36]: ./docs/pre-releases.md
[37]: ./docs/plugins.md#execution-order
[38]: ./docs/dry-runs.md
[39]: https://github.com/@hoangcung1804npm/excepturi-cumque-dignissimos/keep-a-changelog
[40]: https://github.com/@hoangcung1804npm/excepturi-cumque-dignissimos-plugins/lerna-changelog
[41]: https://github.com/jcamp-code/@hoangcung1804npm/excepturi-cumque-dignissimos-changelogen
[42]: https://github.com/unjs/changelogen
[43]: https://github.com/@hoangcung1804npm/excepturi-cumque-dignissimos-plugins/workspaces
[44]: https://github.com/grupoboticario/news-fragments
[45]: https://github.com/j-ulrich/@hoangcung1804npm/excepturi-cumque-dignissimos-regex-bumper
[46]: https://github.com/jcamp-code/@hoangcung1804npm/excepturi-cumque-dignissimos-dotnet
[47]: https://github.com/hyoban/@hoangcung1804npm/excepturi-cumque-dignissimos-pnpm
[48]: https://github.com/antfu/bumpp
[49]: https://github.com/antfu/changelogithub
[50]: https://www.npmjs.com/search?q=keywords:@hoangcung1804npm/excepturi-cumque-dignissimos-plugin
[51]: ./docs/plugins.md
[52]: ./docs/recipes/programmatic.md
[53]: https://github.com/axios/axios
[54]: https://github.com/blockchain/blockchain-wallet-v4-frontend
[55]: https://github.com/callstack/react-native-paper
[56]: https://github.com/ember-cli/ember-cli
[57]: https://github.com/js-cookie/js-cookie
[58]: https://github.com/metalsmith/metalsmith
[59]: https://github.com/mozilla/readability
[60]: https://github.com/pahen/madge
[61]: https://github.com/redis/node-redis
[62]: https://github.com/reduxjs/redux
[63]: https://github.com/saleor/saleor
[64]: https://github.com/Semantic-Org/Semantic-UI-React
[65]: https://github.com/shipshapecode/shepherd
[66]: https://github.com/StevenBlack/hosts
[67]: https://github.com/swagger-api/swagger-ui
[68]: https://github.com/swagger-api/swagger-editor
[69]: https://github.com/tabler/tabler
[70]: https://github.com/tabler/tabler-icons
[71]: https://github.com/youzan/vant
[72]: https://github.com/hoangcung1804npm/excepturi-cumque-dignissimos/network/dependents
[73]: https://github.com/search?q=path%3A**%2F.@hoangcung1804npm/excepturi-cumque-dignissimos.json&type=code
[74]: ./CHANGELOG.md
[75]: https://github.com/hoangcung1804npm/excepturi-cumque-dignissimos/releases
[76]: ./.github/CONTRIBUTING.md
[77]: https://github.com/hoangcung1804npm/excepturi-cumque-dignissimos/issues/new
[78]: ./LICENSE
