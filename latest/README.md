![dotenvx](https://dotenvx.com/better-banner.png)

*a better dotenv*–from the creator of [`dotenv`](https://github.com/motdotla/dotenv).

* run anywhere (cross-platform)
* multi-environment
* encrypted envs

&nbsp;


### Quickstart

Install and use it in code just like `dotenv`.

```sh
npm install @dotenvx/dotenvx --save
```
```js
// index.js
require('@dotenvx/dotenvx').config()

console.log(`Hello ${process.env.HELLO}`)
```

&nbsp;

Or install globally

```sh
brew install dotenvx/brew/dotenvx
```
> * [other global ways to install](https://dotenvx.com/docs/install)
>
> Intall globally as a cli to unlock dotenv for ANY language, framework, or platform. 💥
>
> I am using (and recommending) this approach going forward. – [motdotla](https://github.com/motdotla)

&nbsp;

## Run Anywhere

```sh
$ echo "HELLO=World" > .env
$ echo "console.log('Hello ' + process.env.HELLO)" > index.js

$ node index.js
Hello undefined

$ dotenvx run -- node index.js
Hello World
> :-D
```

see [extended quickstart guide](https://dotenvx.com/docs/quickstart)

More examples

* <details><summary>TypeScript 📘</summary><br>

  ```json
  // package.json
  {
    "type": "module",
    "dependencies": {
      "chalk": "^5.3.0"
    }
  }
  ```

  ```js
  // index.ts
  import chalk from 'chalk'
  console.log(chalk.blue(`Hello ${process.env.HELLO}`))
  ```

  ```sh
  $ npm install
  $ echo "HELLO=World" > .env

  $ dotenvx run -- npx tsx index.ts
  Hello World
  ```

  </details>

* <details><summary>Deno 🦕</summary><br>

  ```sh
  $ echo "HELLO=World" > .env
  $ echo "console.log('Hello ' + Deno.env.get('HELLO'))" > index.ts

  $ deno run --allow-env index.ts
  Hello undefined

  $ dotenvx run -- deno run --allow-env index.ts
  Hello World
  ```

* <details><summary>Bun 🥟</summary><br>

  ```sh
  $ echo "HELLO=Test" > .env.test
  $ echo "console.log('Hello ' + process.env.HELLO)" > index.js

  $ bun index.js
  Hello undefined

  $ dotenvx run -f .env.test -- bun index.js
  Hello Test
  ```

* <details><summary>Python 🐍</summary><br>

  ```sh
  $ echo "HELLO=World" > .env
  $ echo 'import os;print("Hello " + os.getenv("HELLO", ""))' > index.py

  $ dotenvx run -- python3 index.py
  Hello World
  ```

  see [extended python guide](https://dotenvx.com/docs/quickstart)

  </details>
* <details><summary>PHP 🐘</summary><br>

  ```sh
  $ echo "HELLO=World" > .env
  $ echo '<?php echo "Hello {$_SERVER["HELLO"]}\n";' > index.php

  $ dotenvx run -- php index.php
  Hello World
  ```

  see [extended php guide](https://dotenvx.com/docs/quickstart)

  </details>
* <details><summary>Ruby 💎</summary><br>

  ```sh
  $ echo "HELLO=World" > .env
  $ echo 'puts "Hello #{ENV["HELLO"]}"' > index.rb

  $ dotenvx run -- ruby index.rb
  Hello World
  ```

  see [extended ruby guide](https://dotenvx.com/docs/quickstart)

  </details>
* <details><summary>Go 🐹</summary><br>

  ```sh
  $ echo "HELLO=World" > .env
  $ echo 'package main; import ("fmt"; "os"); func main() { fmt.Printf("Hello %s\n", os.Getenv("HELLO")) }' > main.go

  $ dotenvx run -- go run main.go
  Hello World
  ```

  see [extended go guide](https://dotenvx.com/docs/quickstart)

  </details>
* <details><summary>Rust 🦀</summary><br>

  ```sh
  $ echo "HELLO=World" > .env
  $ echo 'fn main() {let hello = std::env::var("HELLO").unwrap_or("".to_string());println!("Hello {hello}");}' > src/main.rs

  $ dotenvx run -- cargo run
  Hello World
  ```

  see [extended rust guide](https://dotenvx.com/docs/quickstart)

  </details>
* <details><summary>Java ☕️</summary><br>

  ```sh
  $ echo "HELLO=World" > .env
  $ echo 'public class Index { public static void main(String[] args) { System.out.println("Hello " + System.getenv("HELLO")); } }' > index.java

  $ dotenvx run -- java index.java
  Hello World
  ```

  </details>
* <details><summary>.NET 🔵</summary><br>

  ```sh
  $ dotnet new console -n HelloWorld -o HelloWorld
  $ cd HelloWorld
  $ echo "HELLO=World" > .env
  $ echo 'Console.WriteLine($"Hello {Environment.GetEnvironmentVariable("HELLO")}");' > Program.cs

  $ dotenvx run -- dotnet run
  Hello World
  ```

  </details>
* <details><summary>Bash 🖥️</summary><br>

  ```sh
  $ echo "HELLO=World" > .env

  $ dotenvx run --quiet -- sh -c 'echo Hello $HELLO'
  Hello World
  ```

  </details>
* <details><summary>Cron ⏰</summary><br>

  ```sh
  # run every day at 8am
  0 8 * * * dotenvx run -- /path/to/myscript.sh
  ```

  </details>
* <details><summary>Frameworks ▲</summary><br>

  ```sh
  $ dotenvx run -- next dev
  $ dotenvx run -- npm start
  $ dotenvx run -- bin/rails s
  $ dotenvx run -- php artisan serve
  ```

  see [framework guides](https://dotenvx.com/docs#frameworks)

  </details>
* <details><summary>Docker 🐳</summary><br>

  ```sh
  $ docker run -it --rm -v $(pwd):/app dotenv/dotenvx run -- node index.js
  ```

  Or in any image:

  ```sh
  FROM node:latest
  RUN echo "HELLO=World" > .env && echo "console.log('Hello ' + process.env.HELLO)" > index.js
  RUN curl -fsS https://dotenvx.sh/ | sh
  CMD ["dotenvx", "run", "--", "echo", "Hello $HELLO"]
  ```

  see [docker guide](https://dotenvx.com/docs/platforms/docker)

  </details>

* <details><summary>CI/CDs 🐙</summary><br>

  ```yaml
  name: build
  on: [push]
  jobs:
    build:
      runs-on: ubuntu-latest
      steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: 16
      - run: curl -fsS https://dotenvx.sh/ | sh
      - run: dotenvx run -- node build.js
        env:
          DOTENV_KEY: ${{ secrets.DOTENV_KEY }}
  ```

  see [github actions guide](https://dotenvx.com/docs/cis/github-actions)

  </details>
* <details><summary>Platforms</summary><br>

  ```sh
  # heroku
  heroku buildpacks:add https://github.com/dotenvx/heroku-buildpack-dotenvx

  # docker
  RUN curl -fsS https://dotenvx.sh/ | sh

  # vercel
  npm install @dotenvx/dotenvx --save
  ```

  see [platform guides](https://dotenvx.com/docs#platforms)

  </details>
* <details><summary>Process Managers</summary><br>

  ```js
  // pm2
  "scripts": {
    "start": "dotenvx run -- pm2-runtime start ecosystem.config.js --env production"
  },
  ```

  see [process manager guides](https://dotenvx.com/docs#process-managers)

  </details>

* <details><summary>npx</summary><br>

  ```sh
  # alternatively use npx
  $ npx @dotenvx/dotenvx run -- node index.js
  $ npx @dotenvx/dotenvx run -- next dev
  $ npx @dotenvx/dotenvx run -- npm start
  ```

  </details>
* <details><summary>npm</summary><br>

  ```sh
  $ npm install @dotenvx/dotenvx --save
  ```

  ```json
  {
    "scripts": {
      "start": "./node_modules/.bin/dotenvx run -- node index.js"
    },
    "dependencies": {
      "@dotenvx/dotenvx": "^0.5.0"
    }
  }
  ```

  ```sh
  $ npm run start

  > start
  > ./node_modules/.bin/dotenvx run -- node index.js

  [dotenvx][info] loading env (1) from .env
  Hello World
  ```

  </details>

* <details><summary>Git</summary><br>

  ```sh
  # use as a git submodule
  $ git dotenvx run -- node index.js
  $ git dotenvx run -- next dev
  $ git dotenvx run -- npm start
  ```

  </details>
* <details><summary>Variable Expansion</summary><br>

  Reference and expand variables already on your machine for use in your .env file.

  ```ini
  # .env
  USERNAME="username"
  DATABASE_URL="postgres://${USERNAME}@localhost/my_database"
  ```
  ```js
  // index.js
  console.log('DATABASE_URL', process.env.DATABASE_URL)
  ```
  ```sh
  $ dotenvx run --debug -- node index.js
  [dotenvx@0.14.1] injecting env (2) from .env
  DATABASE_URL postgres://username@localhost/my_database
  ```

  </details>
* <details><summary>Command Substitution</summary><br>

  Add the output of a command to one of your variables in your .env file.

  ```ini
  # .env
  DATABASE_URL="postgres://$(whoami)@localhost/my_database"
  ```
  ```js
  // index.js
  console.log('DATABASE_URL', process.env.DATABASE_URL)
  ```
  ```sh
  $ dotenvx run --debug -- node index.js
  [dotenvx@0.14.1] injecting env (1) from .env
  DATABASE_URL postgres://yourusername@localhost/my_database
  ```

  </details>


&nbsp;

## Multiple Environments

> Create a `.env.production` file and use `-f` to load it. It's straightforward, yet flexible.
```sh
$ echo "HELLO=production" > .env.production
$ echo "console.log('Hello ' + process.env.HELLO)" > index.js

$ dotenvx run -f .env.production -- node index.js
[dotenvx][info] loading env (1) from .env.production
Hello production
> ^^
```

More examples

* <details><summary>multiple `.env` files</summary><br>

  ```sh
  $ echo "HELLO=local" > .env.local

  $ echo "HELLO=World" > .env

  $ dotenvx run -f .env.local -f .env -- node index.js
  [dotenvx][info] loading env (1) from .env.local,.env
  Hello local
  ```

  </details>

* <details><summary>`--overload` flag</summary><br>

  ```sh
  $ echo "HELLO=local" > .env.local

  $ echo "HELLO=World" > .env

  $ dotenvx run -f .env.local -f .env --overload -- node index.js
  [dotenvx][info] loading env (1) from .env.local,.env
  Hello World
  ```

* <details><summary>`--verbose` flag</summary><br>

  ```sh
  $ echo "HELLO=production" > .env.production

  $ dotenvx run -f .env.production --verbose -- node index.js
  [dotenvx][verbose] injecting env from /path/to/.env.production
  [dotenvx][verbose] HELLO set
  [dotenvx][info] loading env (1) from .env.production
  Hello production
  ```

* <details><summary>`--debug` flag</summary><br>

  ```sh
  $ echo "HELLO=production" > .env.production

  $ dotenvx run -f .env.production --debug -- node index.js
  [dotenvx][debug] configuring options
  [dotenvx][debug] {"envFile":[".env.production"]}
  [dotenvx][verbose] injecting env from /path/to/.env.production
  [dotenvx][debug] reading env from /path/to/.env.production
  [dotenvx][debug] parsing env from /path/to/.env.production
  [dotenvx][debug] {"HELLO":"production"}
  [dotenvx][debug] writing env from /path/to/.env.production
  [dotenvx][verbose] HELLO set
  [dotenvx][debug] HELLO set to production
  [dotenvx][info] loading env (1) from .env.production
  Hello production
  ```

  </details>
* <details><summary>`--quiet` flag</summary><br>

  Use `--quiet` to suppress all output (except errors).

  ```sh
  $ echo "HELLO=production" > .env.production

  $ dotenvx run -f .env.production --quiet -- node index.js
  Hello production
  ```

  </details>
* <details><summary>`--log-level` flag</summary><br>

  Set `--log-level` to whatever you wish. For example, to supress warnings (risky), set log level to `error`:

  ```sh
  $ echo "HELLO=production" > .env.production

  $ dotenvx run -f .env.production --log-level=error -- node index.js
  Hello production
  ```

  Available log levels are `error, warn, info, verbose, debug, silly`

  </details>
* <details><summary>`--convention` flag</summary><br>

  Want to load envs conveniently usng the same convention as Next.js? Set `--convention` to `nextjs`:

  ```sh
  $ echo "HELLO=development local" > .env.development.local
  $ echo "HELLO=local" > .env.local
  $ echo "HELLO=development" > .env.development
  $ echo "HELLO=env" > .env

  $ dotenvx run --convention=nextjs -- node index.js
  Hello development local
  ```

  See [next.js environment variable load order](https://nextjs.org/docs/pages/building-your-application/configuring/environment-variables#environment-variable-load-order)

  (more conventions available upon request)

  </details>

&nbsp;

## Encryption

> Add encryption to your `.env` files with a single command. Pass the `--encrypt` flag.

```sh
$ dotenvx set HELLO World --encrypt
set HELLO with encryption (.env)
```

![](https://github.com/dotenvx/dotenvx/assets/3848/21f7a529-7a40-44e4-87d4-a72e1637b702)

> A `DOTENV_PUBLIC_KEY` (encryption key) and a `DOTENV_PRIVATE_KEY` (decryption key) is generated using the same public-key cryptography as [Bitcoin](https://en.bitcoin.it/wiki/Secp256k1).

More examples

* <details><summary>`.env`</summary><br>

  ```sh
  $ dotenvx set HELLO World --encrypt
  $ echo "console.log('Hello ' + process.env.HELLO)" > index.js

  $ dotenvx run -- node index.js
  [dotenvx] injecting env (2) from .env
  Hello World
  ```

* <details><summary>`.env.production`</summary><br>

  ```sh
  $ dotenvx set HELLO Production --encrypt -f .env.production
  $ echo "console.log('Hello ' + process.env.HELLO)" > index.js

  $ DOTENV_PRIVATE_KEY_PRODUCTION="<.env.production private key>" dotenvx run -- node index.js
  [dotenvx] injecting env (2) from .env.production
  Hello Production
  ```

  Note the `DOTENV_PRIVATE_KEY_PRODUCTION` ends with `_PRODUCTION`. This instructs `dotenvx run` to load the `.env.production` file.

* <details><summary>`.env.ci`</summary><br>

  ```sh
  $ dotenvx set HELLO Ci --encrypt -f .env.ci
  $ echo "console.log('Hello ' + process.env.HELLO)" > index.js

  $ DOTENV_PRIVATE_KEY_CI="<.env.ci private key>" dotenvx run -- node index.js
  [dotenvx] injecting env (2) from .env.ci
  Hello Ci
  ```

  Note the `DOTENV_PRIVATE_KEY_CI` ends with `_CI`. This instructs `dotenvx run` to load the `.env.ci` file. See the pattern?

* <details><summary>combine multiple encrypted .env files</summary><br>

  ```sh
  $ dotenvx set HELLO World --encrypt -f .env
  $ dotenvx set HELLO Production --encrypt -f .env.production
  $ echo "console.log('Hello ' + process.env.HELLO)" > index.js

  $ DOTENV_PRIVATE_KEY="<.env private key>" DOTENV_PRIVATE_KEY_PRODUCTION="<.env.production private key>" dotenvx run -- node index.js
  [dotenvx] injecting env (3) from .env, .env.production
  Hello World
  ```

  Note the `DOTENV_PRIVATE_KEY` instructs `dotenvx run` to load the `.env` file and the `DOTENV_PRIVATE_KEY_PRODUCTION` instructs it to load the `.env.production` file. See the pattern?

* <details><summary>other curves</summary><br>

  > `secp256k1` is a well-known and battle tested curve, in use with Bitcoin and other cryptocurrencies, but we are open to adding support for more curves.
  > 
  > If your organization's compliance department requires [NIST approved curves](https://csrc.nist.gov/projects/elliptic-curve-cryptography) or other curves like `curve25519`, please reach out at [security@dotenvx.com](mailto:security@dotenvx.com).

&nbsp;

## More features

> Keep your `.env` files safe

* [`dotenvx genexample`](https://dotenvx.com/docs/features/genexample) – generate `.env.example` file
* [`dotenvx gitignore`](https://dotenvx.com/docs/features/gitignore) – gitignore your `.env` files
* [`dotenvx prebuild`](https://dotenvx.com/docs/features/prebuild) – prevent `.env` files from being built into your docker container
* [`dotenvx precommit`](https://dotenvx.com/docs/features/precommit) – prevent `.env` files from being committed to code
* [`dotenvx scan`](https://dotenvx.com/docs/features/scan) – scan for leaked secrets in code

> Convenience

* [`dotenvx get`](https://dotenvx.com/docs/features/get) – return a single environment variable
* [`dotenvx set`](https://dotenvx.com/docs/features/set) – set a single environment variable
* [`dotenvx ls`](https://dotenvx.com/docs/features/ls) – list all .env files in your repo
* [`dotenvx status`](https://dotenvx.com/docs/features/status) – compare your .env* content(s) to your .env.vault decrypted content(s)
* [`dotenvx settings`](https://dotenvx.com/docs/features/settings) – print current dotenvx settings

&nbsp;

## Guides

* [quickstart guides](https://dotenvx.com/docs/quickstart)
  * [run anywhere](https://dotenvx.com/docs/quickstart/run)
  * [multi-environment](https://dotenvx.com/docs/quickstart/environments)
  * [encrypted envs](https://dotenvx.com/docs/quickstart/encryption)
* [dotenvx/docs](https://dotenvx.com/docs)
  * [languages](https://dotenvx.com/docs#languages)
  * [frameworks](https://dotenvx.com/docs#frameworks)
  * [platforms](https://dotenvx.com/docs#platforms)
  * [ci/cd](https://dotenvx.com/docs#cis)

&nbsp;

## FAQ

#### Why am I getting the error `node: .env: not found`?

You are using Node 20 or greater and it adds a differing implementation of `--env-file` flag support. Rather than warn on a missing `.env` file (like dotenv has historically done), it raises an error: `node: .env: not found`.

This fix is easy. Replace `--env-file` with `-f`.

```bash
# from this:
./node_modules/.bin/dotenvx run --env-file .env -- yourcommand
# to this:
./node_modules/.bin/dotenvx run -f .env -- yourcommand
```

[more context](https://github.com/dotenvx/dotenvx/issues/131)

#### What happened to the `.env.vault` file?

I've decided we should sunset it as a technological solution to this.

The `.env.vault` file got us far, but it had limitations such as:

* *Pull Requests* - it was difficult to tell which key had been changed
* *Security* - there was no mechanism to give a teammate the ability to encrypt without also giving them the ability to decrypt. Sometimes you just want to let a contractor encrypt a new value, but you don't want them to know the rest of the secrets.
* *Conceptual* - it takes more mental energy to understand the `.env.vault` format. Encrypted values inside a `.env` file is easier to quickly grasp.
* *Combining Multiple Files* - there was simply no mechanism to do this well with the `.env.vault` file format.

That said, the `.env.vault` tooling will still stick around for at least 1 year under `dotenvx vault` parent command. I'm still using it in projects as are many thousands of other people.

#### Will you provide a migration tool to quickly switch `.env.vault` files to encrypted `.env` files?

Yes. Working on this soon.

&nbsp;

## Contributing

You can fork this repo and create [pull requests](https://github.com/dotenvx/dotenvx/pulls) or if you have questions or feedback:

* [github.com/dotenvx/dotenvx](https://github.com/dotenvx/dotenvx/issues) - bugs and discussions
* [@dotenvx 𝕏](https://x.com/dotenvx) (DMs are open)
