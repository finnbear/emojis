# emojis

[![Crates.io Version](https://img.shields.io/crates/v/emojis.svg)](https://crates.io/crates/emojis)
[![Docs.rs Latest](https://img.shields.io/badge/docs.rs-latest-blue.svg)](https://docs.rs/emojis)
[![Build Status](https://img.shields.io/github/workflow/status/rossmacarthur/emojis/build/trunk)](https://github.com/rossmacarthur/emojis/actions?query=workflow%3Abuild)

✨ Lookup and iterate over emoji names, shortcodes, and groups.

### Features

- Lookup up emoji by Unicode value.
- Lookup up emoji by GitHub shortcode.
- Iterate over emojis in recommended order.
- Iterate over emojis in an emoji group. E.g. "Smileys & Emotion" or "Flags".
- Iterate over the skin tones for an emoji.
- Uses Unicode emoji spec (v13.1).

## Examples

```rust
let hand = emojis::lookup("🤌")?;
// Or
let hand = emojis::lookup("pinched_fingers")?;

assert_eq!(hand.as_str(), "\u{1f90c}");
assert_eq!(hand.name(), "pinched fingers");
assert_eq!(hand.group(), emojis::Group::PeopleAndBody);
assert_eq!(hand.shortcode()?, "pinched_fingers");
assert_eq!(hand.skin_tone()?, emojis::SkinTone::Default);

// iterate over all the emojis.
let smiley = emojis::iter().next()?;
assert_eq!(smiley, "😀");

// iterate over all the emojis in a group.
let grapes = emojis::Group::FoodAndDrink.emojis().next()?;
assert_eq!(grapes, "🍇");

// iterate over the skin tones for an emoji.
let raised_hands = emojis::lookup("🙌🏼")?;
let iter = raised_hands.skin_tones()?;
let skin_tones: Vec<_> = iter.map(emojis::Emoji::as_str).collect();
assert_eq!(skin_tones, ["🙌", "🙌🏻", "🙌🏼", "🙌🏽", "🙌🏾", "🙌🏿"]);
```

## License

Licensed under either of

- Apache License, Version 2.0 ([LICENSE-APACHE](LICENSE-APACHE) or
  http://www.apache.org/licenses/LICENSE-2.0)
- MIT license ([LICENSE-MIT](LICENSE-MIT) or http://opensource.org/licenses/MIT)

at your option.
