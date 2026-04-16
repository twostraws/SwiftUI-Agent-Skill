<p align="center">
    <img src="assets/logo.svg" alt="SwiftUI Pro - Agent Skill for Claude Code, Codex, and Gemini" height="100" />
</p>

<h1 align="center">SwiftUI Agent Skill for AI Coding Assistants</h1>

<p align="center">
    <img src="https://img.shields.io/badge/iOS-26+-2980b9.svg" alt="Designed for iOS 26 and later." />
    <img src="https://img.shields.io/badge/swift-6.2+-8e44ad.svg" alt="Designed for Swift 6.2 and later." />
    <a href="https://twitter.com/twostraws">
        <img src="https://img.shields.io/badge/Contact-@twostraws-95a5a6.svg?style=flat" alt="Twitter: @twostraws" />
    </a>
</p>

An agent skill that helps AI coding assistants write smarter, simpler, and more modern SwiftUI, including guidance on API usage, design, performance, and accessibility. Covers navigation, layout, animations, state management, VoiceOver, deprecated API, and more, targeting the mistakes LLMs actually make.

Also available:

- [SwiftData Pro](https://github.com/twostraws/SwiftData-Agent-Skill)
- [Swift Concurrency Pro](https://github.com/twostraws/Swift-Concurrency-Agent-Skill)
- [Swift Testing Pro](https://github.com/twostraws/Swift-Testing-Agent-Skill)

Find more agent skills for Swift and Apple platform development at [Swift Agent Skills](https://github.com/twostraws/Swift-Agent-Skills).

The skill builds upon my existing [AGENTS.md](https://github.com/twostraws/SwiftAgents) file, meaning that you can bring years of knowledge and practical experience into your coding agent of choice in just a few minutes. It uses the [Agent Skills](https://agentskills.io/home) format, so it works smoothly with Claude Code, Codex, Gemini, Cursor, and more.


## Installing SwiftUI Pro

### Claude Code

Add the SwiftUI Agent Skill marketplace, then install the plugin:

```
/plugin marketplace add twostraws/SwiftUI-Agent-Skill
/plugin install swiftui-pro@swiftui-agent-skill
```

### Codex, Gemini, Cursor, and others

```bash
npx skills add https://github.com/twostraws/swiftui-agent-skill --skill swiftui-pro
```

If you get the error `npx: command not found`, it means you don’t currently have Node installed. You need to run this command to install Node through Homebrew:

```bash
brew install node
```

And if *that* fails it usually means you need to [install Homebrew](https://brew.sh) first.

When using `npx`, you can select exactly which agents you want to use during the installation. You can also select whether the skill should be installed just for one project, or whether it should be made available for all your projects.

Alternatively, you can clone this whole repository and install it however you want.

If you’re using Xcode, watch the YouTube video on [How to Install and Use Agent Skills in Xcode](https://www.youtube.com/watch?v=nKVZBKoB6P4) for a walkthrough.


## Using SwiftUI Pro

The skill is called SwiftUI Pro, and can be triggered in various ways. For example, in Claude Code you would use this:

> /swiftui-pro

And in Codex you would use this:

> $swiftui-pro

In both cases you can provide specific instructions if you want only a partial review. For example, `/swiftui-pro Check for deprecated API` on Claude, or `$swiftui-pro Focus on accessibility` in Codex.

You can also trigger the skill using natural language:

> Use the SwiftUI Pro skill to look for performance problems in this project.


## Why Use an Agent Skill for SwiftUI?

This skill is built on thousands of hours of learning, experimenting, and building real-world SwiftUI projects. The rules contained here directly target common SwiftUI mistakes made by LLMs. They sometimes make buttons invisible to VoiceOver, they frequently use deprecated API, and they would often write code that causes surprise performance problems.

You can read more about why I created this skill in my article: [SwiftUI Agent Skill - Write better code with Claude, Codex, and other AI tools](https://www.hackingwithswift.com/articles/282/swiftui-agent-skill-claude-codex-ai).


## Contributing

I welcome all contributions, whether that's adding new checks, improving existing checks, or editing this README – everyone is welcome!

- Keep your Markdown concise. There is a token cost to using skills, particularly with SKILL.md, so please respect the token budgets of users.
- Do not repeat things that LLMs already know, because it burns tokens for no benefit. Focus on edge cases, surprises, soft deprecations, and similar.
- All work must be licensed under the MIT license so it can benefit the most people.

Please ensure you abide by the [Code of Conduct](CODE_OF_CONDUCT.md).


## License

SwiftUI Pro was originally created by [Paul Hudson](https://twitter.com/twostraws), who writes [free Swift tutorials over at Hacking with Swift](https://www.hackingwithswift.com). It’s available under the [MIT License](LICENSE), which permits commercial use, modification, distribution, and private use.


<p align="center">
    <a href="https://www.hackingwithswift.com/plus">
    <img src="https://www.hackingwithswift.com/img/hws-plus-banner@2x.jpg" alt="Hacking with Swift+ logo" style="max-width: 100%;" /></a>
</p>

<p align="center">&nbsp;</p>

<p align="center">
    <a href="https://www.hackingwithswift.com"><img src="https://www.hackingwithswift.com/img/hws-button@2x.png" alt="Hacking with Swift logo" width="66" height="75" /></a><br />
    A Hacking with Swift Project
</p>
