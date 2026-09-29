# hermes-plugin-gemini-image

Native Google AI Studio (Gemini / "Nano Banana") image generation and editing for
[Hermes Agent](https://github.com/NousResearch/hermes-agent). Calls
`generativelanguage.googleapis.com` directly with your own API key. No FAL, OpenRouter, or
gateway account needed.

## Models

| Model | Notes |
| --- | --- |
| `gemini-3.1-flash-image` (default) | Nano Banana 2. 14 aspect ratios, 512/1K/2K/4K, Google Search grounding, up to 14 reference images |
| `gemini-3.1-flash-lite-image` | Fastest and cheapest. 10 aspect ratios, 1K only |
| `gemini-3-pro-image` | Nano Banana Pro. Highest fidelity, 1K/2K/4K, search grounding |

Any other Gemini image model id works too (sent with conservative settings).

## Requirements

- A Google AI Studio API key **with billing enabled**. The free tier has an image quota of 0.
- Set `GOOGLE_API_KEY` (or `GEMINI_API_KEY`) in `~/.hermes/.env`.

## Install

    hermes plugins install semirkabir/hermes-plugin-gemini-image
    hermes plugins enable gemini-image
    hermes config set image_gen.provider gemini

## Config (`config.yaml`)

    image_gen:
      provider: gemini
      gemini:
        model: gemini-3.1-flash-image   # optional
        image_size: 2K                  # optional: 512 | 1K | 2K | 4K
        aspect_ratio: "21:9"            # optional exact ratio
        google_search: false            # optional search grounding
        key_env: GOOGLE_API_KEY         # optional: read the key from another env var
        base_url: ""                    # optional endpoint override

## Tests

    PYTHONPATH=/path/to/hermes-agent pytest tests

## Credits

The provider code is gabbyong's work from NousResearch/hermes-agent PR #120851 (building on
wesleysimplicio's #97576), which the maintainers closed under a "no vendor image backends in
core" policy and asked to be published as a standalone plugin. Ported here with the review
findings from that PR fixed: single-key picker readiness, non-secret env knobs moved to
`config.yaml`, and the `paid` badge. MIT licensed.
