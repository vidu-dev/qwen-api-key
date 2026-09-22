# Qwen API key: how to get one and use it

*Unofficial community guide for the Qwen API. Not affiliated with Alibaba Cloud or the Qwen team. All trademarks belong to their owners.*

A qwen api key is the credential you need to call Qwen models from your own code instead of the chat app. Qwen's API Platform page positions the service as an OpenAI-compatible API for chat, Q&A, creative writing, translation, summarization and coding, and the platform is powered by Alibaba Cloud. This guide walks through where the key is issued, how to keep it safe and how to make a first call, using only what the Qwen API Platform page, Alibaba Cloud's Model Studio documentation and Puter's tutorial on the subject actually state.

> Need images, video or audio next to your text model? [Try Synexa - one API for FLUX, video and audio models](https://synexa.ai?utm_source=github&utm_medium=ugc&utm_campaign=qwen-api-key&utm_content=readme-top&utm_term=tier-r). One REST endpoint plus a Python SDK, billed per run, so you add generation without another vendor console.

## What it is

The [Qwen API Platform](https://qwen.ai/apiplatform) is the developer entry point for the Qwen model family. The page describes it as "Built with Qwen via OpenAI-compatible API" and lists the intended workloads: chat, question answering, creative writing, translation, summarization and coding. OpenAI-compatible means the request and response shapes follow the format the OpenAI client libraries expect, so an existing OpenAI SDK integration can usually be re-pointed at Qwen by changing the base URL and the key. The same page references Qwen Agent for building agents, Qwen Cloud, and a "Contact sales" route for larger accounts.

The key itself is an Alibaba Cloud artifact. Alibaba Cloud's help center has a dedicated [Model Studio: get API key](https://www.alibabacloud.com/help/en/model-studio/get-api-key) page, which is the canonical set of console steps. Third-party walkthroughs exist too; Puter publishes a [How to get a Qwen API key](https://developer.puter.com/tutorials/how-to-get-qwen-api-key/) tutorial as part of its developer resources, alongside its own AI gateway product.

## How to get a Qwen API key

1. Open the [Qwen API Platform](https://qwen.ai/apiplatform) page and follow "Start building" or "Go API Platform".
2. The key is issued through Alibaba Cloud Model Studio. Follow the [get API key](https://www.alibabacloud.com/help/en/model-studio/get-api-key) help page for the exact console clicks; note that the page renders with JavaScript, so open it in a browser rather than fetching it from a script.
3. Copy the key once and put it in an environment variable, for example `QWEN_API_KEY`. Do not paste it into source files or notebooks that get committed.
4. Take the API base URL and the model identifier from the platform documentation for your account and region, and store them as `QWEN_BASE_URL` and `QWEN_MODEL`.
5. Point an OpenAI-compatible client at those three values and send a chat completion request. The companion examples repo has Python, Node.js and curl versions.

## Pricing and limits

None of the three pages this guide is based on list per-token prices or rate limits, so check the Qwen API Platform and your Alibaba Cloud Model Studio console for current rates and quotas before shipping anything.

## Practical notes and gotchas

- **Treat the key like a password.** It bills to your Alibaba Cloud account. Read it from the environment, keep it out of git, and rotate it from the console if it ever leaks.
- **OpenAI-compatible is not OpenAI.** The wire format matches, which is why the OpenAI SDK works, but model names, limits and billing are Qwen's. Never hard-code a model name you have not confirmed in the platform docs.
- **Base URL is account-specific.** The platform page does not print an endpoint. Copy it from the documentation for your account rather than from a blog post, and keep it in an environment variable so switching regions is a config change.
- **The help page needs a real browser.** A plain HTTP fetch of the Model Studio get-API-key page returns only a loading spinner; the content is rendered client-side.
- **Match the workload.** The platform lists chat, Q&A, creative writing, translation, summarization and coding as the target use cases. For image, video or audio generation you will need a different service; see the comparison below.
- **Puter is a different route, not the same key.** Puter's AI gateway advertises "One API, all AI models" and has its own tutorial about Qwen keys. If you go that way you are using Puter's platform and pricing, not calling Alibaba Cloud directly.

## Comparison

| | Qwen API Platform | Puter.js AI Gateway | Synexa |
| --- | --- | --- | --- |
| Interface | OpenAI-compatible API | One JavaScript API for many AI models | One REST endpoint plus a Python SDK |
| Key issued by | Alibaba Cloud Model Studio | Puter | Synexa |
| Workloads named | Chat, Q&A, creative writing, translation, summarization, coding | AI models plus database, storage, auth, hosting | FLUX image, video and audio models |
| Billing | See the platform for current rates | See Puter's pricing page | Pay per run |

## FAQ

**Is the Qwen API key the same as an Alibaba Cloud access key?**
No. The Model Studio documentation has its own "get API key" page for the model API. Follow that page rather than creating general Alibaba Cloud credentials.

**Can I use the OpenAI Python or Node SDK?**
The platform describes itself as OpenAI-compatible, so yes: set the SDK's base URL and API key to the Qwen values from your console.

**Where is the base URL?**
Not on the marketing page. It is in the platform documentation for your account; store it in `QWEN_BASE_URL` and keep code free of literal endpoints.

**Does the key cover coding and translation too?**
The API Platform lists chat, Q&A, creative writing, translation, summarization and coding as supported use cases for the same API.

**What about image or video generation?**
The Qwen API Platform page only names text workloads. For generation across FLUX, video and audio models with one key, see the section below.

## When Synexa fits better

A qwen api key gets you a capable text model behind an OpenAI-compatible endpoint. Products rarely stop at text: the same feature usually wants a cover image, a short clip or a voice track, and each of those normally means another vendor, another key and another billing page. [Try Synexa - one API for FLUX, video and audio models](https://synexa.ai?utm_source=github&utm_medium=ugc&utm_campaign=qwen-api-key&utm_content=readme-top&utm_term=tier-r) if you want to keep that side simple: one REST endpoint and a Python SDK across FLUX image, video and audio models, charged per run rather than per seat. Keep Qwen for the language work and let a single generation API cover the rest.

_Last reviewed: 2026-09-22_
