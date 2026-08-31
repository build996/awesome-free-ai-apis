# Free AI API Limits

A maintained, no-nonsense reference for the **real free tiers of AI APIs** — LLM inference, image, OCR, and speech — in one place.

Most "free AI API" lists tell you a provider *has* a free tier. They rarely tell you the number that matters: **how much you actually get, whether you can use it commercially, and where the catch is.** This repo does.

> ⚠️ Free tiers change constantly, and several providers (Google, Mistral) have **removed their published limits and hidden them behind a login**. Numbers here are qualitative on purpose where the provider no longer publishes them — always confirm against the linked source before you build on it.

Each row links to a hands-on write-up with runnable code and the current details.

## We measure these ourselves

Vendor docs go stale within weeks, so we benchmark them instead. Our open harness — **[free-ai-api-benchmark](https://github.com/build996/free-ai-api-benchmark)** — runs every provider from a US GitHub Actions runner and measures three things: **generation speed** (from each API's own `usage` token counts), **real quotas** (read from live `x-ratelimit-*` headers, not the docs), and **capability** (four programmatic pass/fail tasks: strict JSON, code, Chinese, long-context retrieval).

What that turned up in **August 2026**:

- **Groq is the speed king** — `gpt-oss-120b` measured at **~525 tok/s**, roughly 3× the next provider. (Smaller models on Groq sometimes report far higher figures, but those runs stream in a single buffered chunk, which inflates the number; we exclude them rather than publish a result we can't stand behind.)
- **OpenRouter served NVIDIA's own `nemotron-3-super-120b` faster than NVIDIA did** — 45.7 vs 36.7 tok/s, and a third of the latency.
- **GitHub Models is dead** (`410`, retired July 30 2026), and **DeepSeek, SambaNova, Together, Cerebras and xAI now all want a card or a deposit**.
- **Gemini 3.6-flash is a reasoning model** — 17–30 seconds of thinking before the first token, so tokens/second is the wrong lens for it.

Full write-up with every number: **[Free AI APIs Tested](https://toolfreebie.com/free-ai-api-speed-test/)**.

---

## Chat / LLM inference APIs

| Provider | What the free tier actually gives you | The catch | Guide |
|---|---|---|---|
| **Groq** | Free API, generous daily limits, OpenAI-compatible; fastest small-model inference | Rate-limited per model; limits tightened over time | [Guide](https://toolfreebie.com/groq-fastest-free-ai-api/) |
| **Cerebras** | Wafer-scale speed on GPT-OSS / Llama; **$5/month trial credit** | **Card now required (2026)** — the old no-card free tier is gone | [Guide](https://toolfreebie.com/cerebras-free-api/) |
| **SambaNova Cloud** | Big models (Llama 3.3 70B, DeepSeek V3.x) at 400+ tok/s | **Card now required (2026)** — we hit `402 PAYMENT_METHOD_REQUIRED`, balance 0 | [Guide](https://toolfreebie.com/sambanova-cloud-free-api/) |
| **Google Gemini** | Genuine free tier, strong models | **Limits now login-gated / unpublished** — you can't plan around them | [Guide](https://toolfreebie.com/gemini-free-ai-api/) |
| **OpenRouter** | `:free` variants of many open models via one OpenAI-compatible endpoint | ~20 req/min, ~50/day free; a one-time $10 credit raises it to ~1,000/day | [Guide](https://toolfreebie.com/openrouter-free-ai-models/) |
| **GLM (Zhipu / Z.ai)** | Three genuinely free models (not expiring trial credits); OpenAI **and** Anthropic compatible | International access via Z.ai | [Guide](https://toolfreebie.com/glm-free-api/) |
| **DeepSeek** | Open weights you can self-host for $0; new accounts get API trial credit | **V3/R1 retired 2026 → V4**; we hit `402 Insufficient Balance` — the hosted API now needs funds | [Guide](https://toolfreebie.com/deepseek-free-api/) |
| **Kimi K2 (Moonshot)** | Open-weights model → free via OpenRouter `:free` or self-host | Moonshot's own endpoint is cheap prepaid, **not** free | [Guide](https://toolfreebie.com/kimi-k2-api-free/) |
| **Qwen3-Coder** | Apache-2.0 open weights; free via OpenRouter `:free` or self-host | Free Qwen OAuth tier was **discontinued 2026-04-15** | [Guide](https://toolfreebie.com/qwen3-coder-free-api/) |
| **Grok (xAI)** | Up to **$150/month** in API credits | Only via opting into the data-sharing program; not free by default | [Guide](https://toolfreebie.com/grok-api-free-credits/) |
| **Mistral** | Free tier + Apache-2.0 open weights (Nemo, Mixtral) | Free-tier limits **went dark** (login-gated) | [Guide](https://toolfreebie.com/mistral-free-api/) |
| **Cohere** | Free trial API — the best free **embedding + rerank** for RAG | Trial keys are rate-limited | [Guide](https://toolfreebie.com/cohere-rag-api/) |
| **Together AI** | Free FLUX.1 [schnell] endpoint behind an OpenAI-compatible key | **Deposit required (2026)** — new accounts land in read-only mode | [Guide](https://toolfreebie.com/together-ai-free-api-llama-deepseek-flux-2026/) |
| **Cloudflare Workers AI** | **10,000 Neurons/day** free, no card; hard-stops instead of billing | Neuron budget is shared across all models | [Guide](https://toolfreebie.com/cloudflare-workers-ai/) |
| ~~**GitHub Models**~~ | ~~Free GPT-4o & Llama for developers~~ | **RETIRED July 30, 2026** — the API returns `410`; we verified it's gone | [What to use instead](https://toolfreebie.com/github-models-free-api/) |
| **NVIDIA NIM** | Free API credits across many models | Credit-capped | [Guide](https://toolfreebie.com/nvidia-nim-free-api/) |
| **Hugging Face** | ~$0.10/mo inference credits + Spaces **ZeroGPU** (time-sliced A100) | Tiny credit, but unlocks thousands of models | [Guide](https://toolfreebie.com/hugging-face-spaces-free-gpu/) |
| **Alibaba Bailian** | Free-tier access to **Qwen & DeepSeek** models via Alibaba's OpenAI-compatible API | Regional access; free quotas modest | [Guide](https://toolfreebie.com/alibaba-bailian-free-api/) |

## Multimodal (image · OCR · speech)

| Task | Best free option | The catch | Guide |
|---|---|---|---|
| **Image generation** | Cloudflare Workers AI (~230 FLUX images/day), Pollinations (keyless) | Commercial use depends on model license (FLUX.1 [schnell] = Apache 2.0, safe) | [Guide](https://toolfreebie.com/free-image-generation-api/) |
| **OCR** | OCR.space (25,000 req/mo, no card) | 1 MB / 3-page file caps | [Guide](https://toolfreebie.com/free-ocr-api-pdf/) |
| **Speech-to-text** | Free Whisper API options compared | Rate/among-provider limits vary | [Guide](https://toolfreebie.com/free-whisper-api-compared/) |
| **Text-to-speech** | Free TTS API options compared | Voice/character caps | [Guide](https://toolfreebie.com/free-text-to-speech-api/) |

## Agent, RAG & LLM tooling

Free APIs and open-source tools that feed and route your models — search, scraping, moderation, and multi-provider gateways.

| Tool | What the free tier gives you | The catch | Guide |
|---|---|---|---|
| **Tavily / Brave / Exa** | Free search APIs built for AI agents (LLM-ready results) | Small monthly quotas; **Brave now needs a card** | [Guide](https://toolfreebie.com/tavily-vs-brave-vs-exa-search/) |
| **Firecrawl** | Free tier to scrape sites into clean, LLM-ready markdown | Monthly page cap on the free plan | [Guide](https://toolfreebie.com/firecrawl-free-scraping-api/) |
| **Crawl4AI** | Open-source (self-host) crawler that outputs LLM-ready data | Self-hosted; you run it | [Guide](https://toolfreebie.com/crawl4ai-free-web-crawler/) |
| **LiteLLM** | Open-source gateway: one OpenAI-compatible API for 100+ LLMs | Self-hosted proxy; you supply provider keys | [Guide](https://toolfreebie.com/litellm-free-llm-gateway/) |
| **Content moderation** | Free content-moderation API options for text | Rate / size limits vary | [Guide](https://toolfreebie.com/free-content-moderation-api/) |

---

## The licensing trap (read this before self-hosting)

"Open source" and "free to use commercially" are **not** the same thing. A repo can carry a permissive **code** license while its **model weights** are revenue-capped. Marker and Surya, for example, are among the most-starred OCR repos on GitHub and both ship revenue-capped weight licenses — while Docling (MIT), Tesseract, PaddleOCR, and RapidOCR (Apache 2.0) are commercially safe. **Always check the weights license, not just the code badge.**

## How to pick

- **Fastest small-model responses →** Groq — we measured `gpt-oss-20b` at **~1,100 tok/s** from a US runner
- **Big models for free →** OpenRouter — its free `nemotron-3-super-120b` beat NVIDIA's own API in our test
- **One key, many models →** OpenRouter
- **RAG (embed + rerank) →** Cohere
- **No rate limit at all →** self-host open weights (Qwen3-Coder, Kimi K2, DeepSeek, Mistral)

Full side-by-side: **[Best Free AI APIs 2026](https://toolfreebie.com/best-free-ai-apis-2026/)** · Speed shootout: **[Groq vs Cerebras vs Gemini](https://toolfreebie.com/groq-vs-cerebras-vs-gemini/)**

---

---

## Related lists

Part of a small set of measured, regularly re-checked references:

| Repo | Covers |
|---|---|
| **[free-ai-api-benchmark](https://github.com/build996/free-ai-api-benchmark)** | The harness behind the numbers here — speed, quotas, agent tasks, weekly runs |
| **[actually-free-hosting](https://github.com/build996/actually-free-hosting)** | Where to *run* what you build: free VPS, PaaS, static and databases |
| **[free-host-speedtest](https://github.com/build996/free-host-speedtest)** | A page for measuring free hosting speed yourself |

Same principle across all of them: **verify, then publish** — and say plainly when a free tier has quietly died.

## Contributing

Found a changed limit, a dead link, or a provider we missed? PRs welcome — see [CONTRIBUTING.md](CONTRIBUTING.md). Keep entries **sourced** (link the provider's own docs) and **qualitative where the provider hides the number**.

## License

[MIT](LICENSE) — data and text free to reuse. Maintained by [Tool Freebie](https://toolfreebie.com).
