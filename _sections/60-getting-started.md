---
anchor: getting-started
title: Getting Started
menu: Getting Started
order: 60
class: getting-started
content_class: install-steps
---
{:ext: target="_blank" rel="noopener"}

### Requisites {#prerequisites}

- [Ruby 3.4.7+](https://www.ruby-lang.org/){:ext} - the knowledge base server is Ruby.
- [MusaDSL](https://musadsl.yeste.studio){:ext} - the framework Nota assists with. Nota reads the copy you install for your own work.
- A [Voyage AI](https://dash.voyageai.com/){:ext} API key, for the embeddings. The free tier is enough for personal use.
- macOS or Windows - on Windows on ARM, use an **x64** Ruby, see [Troubleshooting](#troubleshooting). Linux: to be tested.

### Install {#install}

#### 1. Add your API key

Nota's MCP server runs as a subprocess of your coding agent, and inherits the environment of
whatever launched it. Set the key in two places: the session you have open now, and every
session from now on.

<div class="tabs">
  <div class="tab-triggers">
    <button class="tab-trigger is-active" data-tab="key-macos">macOS</button>
    <button class="tab-trigger" data-tab="key-linux">Linux</button>
    <button class="tab-trigger" data-tab="key-windows">Windows</button>
  </div>

  <div class="tab-panel is-active" id="tab-key-macos">
    <pre><code># this session
export VOYAGE_API_KEY="your-key-here"

# every session from now on
echo 'export VOYAGE_API_KEY="your-key-here"' &gt;&gt; ~/.zshrc</code></pre>
    <p class="note">zsh, the default on macOS. Under bash, the second line goes to <code>~/.bash_profile</code>.</p>
  </div>

  <div class="tab-panel" id="tab-key-linux">
    <pre><code># this session
export VOYAGE_API_KEY="your-key-here"

# every session from now on
echo 'export VOYAGE_API_KEY="your-key-here"' &gt;&gt; ~/.bashrc</code></pre>
    <p class="note">bash, the usual default. Under zsh, the second line goes to <code>~/.zshrc</code>.</p>
  </div>

  <div class="tab-panel" id="tab-key-windows">
    <p class="note">PowerShell</p>
    <pre><code># this session
$env:VOYAGE_API_KEY = 'your-key-here'

# every session from now on
[Environment]::SetEnvironmentVariable('VOYAGE_API_KEY', 'your-key-here', 'User')</code></pre>

    <p class="note">cmd</p>
    <pre><code>:: this session
set VOYAGE_API_KEY=your-key-here

:: every session from now on
setx VOYAGE_API_KEY "your-key-here"</code></pre>
  </div>
</div>

#### 2. Install the plugin

<div class="tabs">
  <div class="tab-triggers">
    <button class="tab-trigger is-active" data-tab="claude-code">Claude Code</button>
    <button class="tab-trigger" data-tab="opencode">opencode (on hold)</button>
  </div>

  <div class="tab-panel is-active" id="tab-claude-code">
    <ol>
      <li>
        Start Claude Code from the terminal where you set the key:
        <pre><code>claude</code></pre>
      </li>
      <li>
        Add the yeste.studio marketplace:
        <pre><code>/plugin marketplace add javier-sy/claude-plugins</code></pre>
      </li>
      <li>
        Install the plugin:
        <pre><code>/plugin install nota@yeste.studio</code></pre>
      </li>
      <li>
        Finish the setup:
        <pre><code>/nota:setup</code></pre>
        <p>
          It reports what is still missing and installs it - about 30 MB, once. Your own
          Ruby is not touched.
        </p>
      </li>
      <li>
        Leave Claude Code. The knowledge base server only starts with a new session:
        <pre><code>/exit</code></pre>
      </li>
      <li>
        Come back to the same conversation:
        <pre><code>claude --continue</code></pre>
      </li>
    </ol>
  </div>

  <div class="tab-panel" id="tab-opencode">
    <div class="notice">
      <strong class="notice__title">On hold</strong>
      <p>
        <strong>Nota is available for Claude Code only.</strong> The opencode channel is on
        hold: npm serves an old release under the previous name
        (<code>nota-plugin-for-opencode</code> 0.11.1), from before most of what Nota does
        now.
      </p>
    </div>
  </div>
</div>

### First questions {#first-questions}

Say **"hello musa"** for the welcome tour, or go straight to
`/nota:explain how does the sequencer work?`

### What gets downloaded {#what-gets-downloaded}

Everything lands in `~/.config/nota/`, and `/nota:setup` brings all
of it: the Ruby dependencies the knowledge base runs on, the 200 KB
`sqlite-vec` extension, and the latest `knowledge.db` - [MusaDSL](https://musadsl.yeste.studio)
documentation, API reference, demos and best practices, pre-indexed with their Voyage
embeddings. Your `private.db` is created empty the first time you index a work
of your own; nothing private leaves your machine.

### License {#license}

- **Free of charge.** Install it and use it, on as many machines as you
  like, for anything - including professional and commercial work.
- **What you make with Nota is yours.** Scores, recordings, analyses and
  code, whether you wrote it or the assistant did: no condition from Nota itself, and
  nothing owed in return. Code that uses [MusaDSL](https://musadsl.yeste.studio) follows MusaDSL's terms like any other:
  composing with it is free of obligation; distributing software built on it means the
  GPL or a commercial license from yeste.studio.
- **The source is not open.** Nota is licensed to be used, not copied,
  modified or redistributed. The terms ship with the plugin, in its `LICENSE`
  file.
- **[MusaDSL](https://musadsl.yeste.studio) is free software**
  ([GPL-3.0-or-later](https://musadsl.yeste.studio/#license){:ext}),
  and so is the knowledge base. Only the assistant is licensed differently.
- **Commercial license.** If you need Nota under terms its license does not
  cover - for instance, inside a closed product - yeste.studio offers a commercial license.
  Write to [javier@yeste.studio](mailto:javier@yeste.studio).

`/nota:license` shows these terms inside your session, and the full text on
request. What binds is that text, not the summary.
{: .note}

### Repository {#repository}

Detailed README and the knowledge base releases:
[<ion-icon name="logo-github"></ion-icon> javier-sy/nota](https://github.com/javier-sy/nota){:ext}

### Troubleshooting {#troubleshooting}

| Symptom | Likely cause / fix |
|---|---|
| `/nota:setup` says Voyage key missing | The key is not in the environment your agent was launched from. Set it, then reopen Claude Code or opencode from a terminal that has it. |
| Knowledge base did not download | Check internet connectivity; `/nota:setup` retries the download. |
| Search returns empty results | The plugin may not have indexed your local works yet - run `/nota:index` on the project root. |
| `Could not find mcp-…` / `sqlite3-…` in locally installed gems | The knowledge base server says this and stops, which is what it is meant to do: the gems are installed by `/nota:setup`, not on startup. Run it, then start Claude Code again - `claude --continue` keeps the conversation. Reloading plugins does not restart an MCP server. |
| The session says the platform is not supported | Windows on ARM: neither `sqlite3` nor `sqlite-vec` publishes a build for it. Install a Ruby built for x64 - Windows runs it under emulation - and set `NOTA_RUBY` to its `ruby.exe` so your other Ruby work keeps the interpreter you have. |
| The sqlite-vec extension did not download | The knowledge base cannot open without it. Check internet connectivity and reopen the session; `/nota:setup` reports the path it resolved and retries. |
| `Missing environment variables: HOME`, and no Nota tools available | Nota 1.0.1 and earlier on Windows. Update the plugin - 1.0.2 no longer asks the editor where your home directory is. |
| MCP server connection failing | Run `/nota:setup`: it reports the Ruby side, the key, the extension and both databases, and names which one is missing. |
{: .libraries-table}

**If installation fails on your platform, open an issue** - especially on
Linux or Windows - at
[<ion-icon name="logo-github"></ion-icon> javier-sy/nota](https://github.com/javier-sy/nota/issues){:ext}
with your operating system, the output of `ruby -v`, and what
`/nota:setup` reports.
